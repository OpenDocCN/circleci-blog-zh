# CircleCI 2.0 现在可以在您的防火墙后使用

> 原文：<https://circleci.com/blog/circleci-2-0-is-now-available-behind-your-firewall/>

**来自出版商的说明:**您已经找到了我们的一些旧内容，这些内容可能已经过时和/或不正确。尝试在[我们的文档](https://circleci.com/docs/)或[博客](https://circleci.com/blog/)中搜索最新信息。

* * *

从今天开始，在防火墙后使用 CircleCI 的客户现在可以访问 CircleCI 2.0 提供的所有功能和性能，包括工作流、完整的 Docker 支持和基于虚拟机的作业。CircleCI 2.0 已于 7 月初[面向我们的云客户](https://circleci.com/blog/launching-today-circleci-2-0-reaches-general-availability/)正式发布，而[对于那些已经切换到 2.0 的客户来说，结果](https://twitter.com/i/moments/877210697834184704)令人印象深刻。

## 2.0 中的新功能

**工作流**
使用灵活的规则来协调任意数量的作业的执行，包括基于 git 分支或标签的作业过滤器，并行、串行或以更复杂的扇入和扇出配置系列运行作业的流量控制，以及需要人工批准的作业的手动门。

**Docker 完全支持**
当我们决定[重新搭建平台](https://circleci.com/blog/why-we-broke-our-philosophical-vows-to-bring-you-circleci-2-0/)我们的构建系统时，我们的口号之一是:如果某个东西在 Docker 上有效，它也应该在 CircleCI 上有效。团队现在可以使用他们自己的定制 Docker 映像作为他们的执行环境，并且可以从他们的工作中完全访问`docker`命令。我们还增加了 Docker 层缓存和其他优化，为您的团队提供他们想要的按需、Docker 友好的 CI/CD 系统。如果您的团队还没有使用 Docker，我们提供了一整套现成的图像，使用所有主要语言，他们可以开箱即用。

**强大的调优选项**
借助我们全新的定制缓存、针对 CPU 和 RAM 的按作业选项、高级并行性和跨作业工作空间，您的团队可以比以前更加精确地优化总构建时间。

**情境**
利用[情境](https://circleci.com/docs/contexts/)，在组织内跨项目共享环境变量很容易。开发人员可以在其工作流配置中通过一行请求在组织范围的上下文中运行作业。

## 将连续性与版本化版本相协调

作为一家以持续为核心的公司，我们相信快速迭代、频繁投入生产以及保持我们的整体高吞吐量。虽然每次我们合并到 master 时，我们的云托管客户都会看到新的更新，但我们知道，大多数运行自己的 CircleCI 安装的客户无法以这种方式运行。

为了确保我们提供一个强大的平台，并让您了解我们最新的功能和修复，我们将定期发布一个稳定的分支。我们不会为 1.x.y 版本发布单独的修补程序版本，因此使用 1.48.x 之前任何版本的客户下次升级时都会迁移到 2.x.y 版本。

此外，我们现在将为那些希望更频繁升级的人提供更多版本节奏选项。如果您的团队对更频繁的发布感兴趣，请联系您的客户团队。

## CircleCI 入门

如果你是 CircleCI 的新用户，我们鼓励你[注册](https://circleci.com/signup/)并尝试一下。如果你准备好开始运行测试[，联系我们在你的防火墙后安装 CircleCI 的试用版](https://circleci.com/contact-us/)。

那些已经安装了 CircleCI 的用户应该确保阅读[发行说明](https://circleci.com/server/changelog/)，因为需要运行一些重要的迁移，这将需要一个很短的维护窗口。您还需要与您的客户团队讨论新的发布渠道，并需要在您的管理控制台中设置一些新的设置。

## “CircleCI 企业”怎么了？

CircleCI 的长期客户会注意到，我们不再使用“CircleCI 企业”这个术语来描述我们的软件。我们发现，企业这个词更适合用来描述那些规模足够大的公司的一般需求，这些公司拥有跨不同业务部门的内部团队生态系统。虽然我们从名称中去掉了“企业”一词，但我们仍然致力于为大型企业提供他们成功所需的全套产品，无论他们如何部署 CircleCI。这包括我们的核心产品、我们的专业客户管理团队以及我们的[高级支持层](https://circleci.com/support/plans/)。

我们希望 CircleCI 对任何规模的团队来说都是同样伟大的产品。无论您是在云中使用 CircleCI，还是在您控制的服务器上安装 circle ci，我们都致力于帮助各种规模的软件组织以可预测性更快地交付价值。