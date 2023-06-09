# 深入 CircleCI 工作区- CircleCI

> 原文：<https://circleci.com/blog/deep-diving-into-circleci-workspaces/>

* * *

这篇文章是我们关于在工作流中保存数据的概述的后续。要了解如何最好地使用工作区、缓存和工件，请在这里阅读我们的介绍性帖子[。](https://circleci.com/blog/persisting-data-in-workflows-when-to-use-caching-artifacts-and-workspaces/)

* * *

工作空间是工作流的一项功能，用于将数据从工作流中的作业移动到后续作业。

![Diagram-v3-Workspaces.png](img/6686752ed5762af1028d4de38cdb9089.png)

“workspace”这个名字可能会让人联想到一个单一存储位置的图像，作业可以随意添加或删除该位置。然而，工作流会在构建过程中引入大量的并发性，并且并发作业的运行没有固定的顺序。在这些情况下，单个可变的存储位置会导致作业在不同的工作流运行中反复失败，因为它们从未获得工作区内容的一致视图。如果您的工作流有并发作业，这将显著影响您获得可重复构建过程的能力。所以工作空间需要从不可变的层构建(我们使用存储在 blob-store 中的 gzipped tarballs)。每个作业可以使用`persist_to_workspace`命令向工作空间添加一个新的不可变层。

但是这还不够，为了可重复性，我们需要能够计算出当一个作业使用`attach_workspace`命令时，它应该能够看到什么工作空间内容。

例如，以下工作流程:

```
workflows:
  version: 2
  jobs:
    - compile-assets
    - compile-code
    - test:
        requires:
          - compile-assets
          - compile-code
    - code-coverage
    - deploy:
        requires:
          - test
          - code-coverage 
```

生成此图(我在作业名称之外用一个字母标记了作业):

```
 +---------------------+
 |  code-coverage (D)  +-------------------------+
 +---------------------+                         |
                                                 |    +--------------+
                                                 +---->  deploy (E)  |
                                                 |    +--------------+
 +----------------------+                        |
 |  compile-assets (A)  +---+                    |
 +----------------------+   |                    |
                            |   +------------+   |
                            +--->  test (C)  +---+
                            |   +------------+
 +--------------------+     |
 |  compile-code (B)  +-----+
 +--------------------+ 
```

作业 C 肯定会看到作业 A 和作业 B 增加的工作空间，但是作业 D 呢？有时作业 D 可能在作业 C 之前运行，有时可能在作业 C 之后运行，没有任何保证。

幸运的是，我们可以求助于工作流图，规则是一个作业只能看到工作流图中上游作业添加到工作区的数据。所以作业 C 永远看不到来自作业 d 的数据。

另一个考虑是，一个作业可以“覆盖”前一个作业存储在工作区中的数据，如果作业 B 和作业 C 都将一个名为`code.jar`的文件以不同的内容存储在工作区中，作业 E 应该看到哪个？

我们再次转向工作流图，由上游作业产生的工作空间层以拓扑顺序被应用，即由作业的祖先产生的层总是在由作业产生的层之前被应用。将工作空间附加到作业 E 时，应用层的一个有效顺序是 A、B、C、D，但另一个完全有效的顺序是 D、B、A、C。

在所有情况下，来自作业 C 的层在来自作业 A 的层之后被应用，因此我们可以知道作业 E 将会看到来自作业 C 的`code.jar`。

最后要考虑的是，当两个并发作业(例如，作业 A 和 B，或者作业 C 和 D)将同一个文件添加到工作区时会发生什么？如果作业 C 和 D 都存储了`code.jar`，作业 E 应该看哪个？工作流图在这里没有帮助，工作是并发的，但是我们希望避免模糊性，并且*绝对*避免在不同的工作流运行中反复无常。因为我们的目标是拥有可重复的工作流，所以我们标记了这种情况，并失败了`attach_workspace`命令，错误突出显示了不明确的文件。

### 使用工作空间重新运行工作流

上面强调的问题和实现可能听起来非常理论化，对于没有任何并发性的简单工作流没有太多实际好处，但是所有这些不变性和如何应用层的仔细排序意味着我们可以在工作流运行之间共享部分工作区*!*

这就是仅重新运行工作流中失败的作业的工作方式，我们可以确定上次运行的成功作业的所有工作空间层，并在重新运行时使用这些层。这将节省您的时间和资源，因为我们不需要再次运行成功的作业。

### 概括起来

*   工作空间旨在将作业期间生成的数据移动到工作流中的后续作业
*   我们可以通过使用不变性和工作流图来确定工作流中的每个作业可以看到哪些数据，从而实现可重复性。
*   工作空间并不神奇；最终它会创建 tarballs 并将它们存储在 blob 存储中。附加工作空间需要为将数据持久化到工作空间的每个上游作业下载和解包 tarballs。

### 这听起来很棒，但是仍然有很多选择——我应该用哪个特性做什么？

首先要记住的是，无论使用哪种特性，您存储的所有内容都有存档、上传和下载的代价。带宽不是无限的，延迟不是零。不要忘记文件系统操作，将几万到几十万个小文件打包和解包到一个归档中需要时间。[脚注:在我的多核 Macbook Pro dev 机器上，采用固态硬盘，没有虚拟化开销，为典型客户的节点包集创建`node_modules`目录的归档只需要 23 秒。]

工作区提供了诱人的便利，将您的整个结帐和依赖关系都放在工作区中，但是这种便利也有缺点:

*   导致所有依赖项的存档和上传
*   导致存档和上传您的整个 git repo(包括历史)
*   即使您已经恢复了缓存，也会导致重新下载这些文件

为了加快工作流程，我们希望最大限度地减少存档、上传、下载和解包操作。

## 你该怎么办？

*   将工作空间用于在作业中生成的、需要供后续作业使用的数据。这是 workspaces 的面包和黄油，在重新运行时工作良好。
*   将依赖关系保存在 CircleCI 缓存中，并使用`restore_cache`将它们复制到容器中。如果您键入依赖清单的校验和(packages.json、Gemfile.lock、project.clj 等),那么您可以避免在每个工作流中归档和上传依赖数据。CircleCI 缓存机制只会在依赖清单的内容发生变化时保存新的缓存。由于依赖关系可能很大和/或有大量文件，这可以节省大量时间。
*   具体说明您在工作空间中保存了什么，以避免存储后续作业不需要的数据。例如，如果您不需要在下游作业中使用`git`，请避免将`.git`添加到您的工作区，它可能包含大量数据。
*   不要在缓存和工作区存储相同的数据，你会付出两次下载的代价。
*   如果你确实需要完整的 git 回购协议，可以考虑使用`checkout`从你的 VCS 供应商那里获得回购协议。这比其他建议更不明确，因为一般网络“天气”对 VCS 提供商到 CircleCI 的转移有更大的影响。
*   对于工作流生成的任何数据，如果您希望在工作流完成后能够在 CircleCI 系统之外访问这些数据，请使用工件。