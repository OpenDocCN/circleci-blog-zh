# 我们如何推出 CircleCI orbs | CircleCI

> 原文：<https://circleci.com/blog/reflections-major-feature-launch/>

### 摘自一位产品经理关于 CircleCI orbs 发布的回顾。

2018 年 11 月，我们[推出 CircleCI orbs](https://circleci.com/blog/announcing-orbs-technology-partner-program/) 。我最近[写了](https://circleci.com/blog/designing-a-package-manager-from-the-ground-up/)关于我们在构建新的包管理器时所做的设计决定。在这里，我想分享一些我们在推出主要新功能时学到的(或重新学到的)经验。你可能不会感到惊讶，我们想了很多关于如何发布工作软件，我们的追溯过程帮助我们把我们观察到的和学到的用语言表达出来。

以下是我们关于 orbs 启动计划的内部回顾的摘录，为公众消费做了一些编辑。
**_ _**_ _*_ _*_ _

摘自题为“值得分享的观察与思考”的一节:

### 投入专门但有限的时间进行内部概念验证是非常宝贵的。

内部截止日期是保持专注于工作原型的巨大动力。在我们的例子中，它也给了我们一个清晰但相当低的“足够好”的标准来测试这个概念。在 CircleCI 2.0 发布后的第一次主要迁移浪潮中，我们对解决引导和管理新配置格式的困难有了新的兴趣。2018 年 3 月(orbs 上市前 8 个月)，我们开始了 orbs 的初步设计工作。

在那段时间，我们还为整个工程组织(来自 11 个州和 10 个国家至少 25 个不同地点的 50 多名工程师)的大型聚会制定了议程。那次会议提供了一个完美的机会:不仅仅是许多不同类型的工程师作为一个被俘虏的、投入的观众解决了无数的问题，而且他们所有人都是他们必须交付的项目中我们平台的用户。像这样的测试有一个短的截止日期比交付生产软件的短的截止日期更容易，因为我们没有做出设计妥协，而是选择妥协一些端到端的功能和润色，以便测试我们最危险的假设。我们投入了我们(当时新成立的)开发人员体验团队一个月的努力，创建了足够的工作软件来测试 orb 的核心设计概念。经过 4 名工程师一个月的投资，仅用了一天时间就迅速获得了对初始设计决策的各种反馈，这让我们不仅可以验证概念的强度，还可以设定目标和优先级，以使 orbs 可以投入生产。

### 在计划开始的时候，有几周的时间从 backlog 交付的责任中抽身出来，进行开放式设计，这是非常宝贵的。

我们花了大量时间进行开放式设计讨论，包括许多具体草图、理论探索和大图概念开发。除了功能细节之外，我们必须围绕 orb 开发发明一个习语，包括形式化我们的术语，以便就 DSL 设计进行富有成效的对话。我们漫无目的地交谈，没有明确的议程，这在商业环境中通常是令人讨厌的。这在当时可能很容易被认为是一种气味，因为团队的速度急剧下降，但是这些种类的抽象和框架对于完成将 orbs 转化为生产就绪软件的工程工作是必不可少的。

### “文件-第一设计”运作良好。

你可能听说过这样的故事，亚马逊在早期使用一种模式[在产品计划开始之前而不是之后写新闻稿](https://www.quora.com/What-is-Amazons-approach-to-product-development-and-product-management)，作为展示最终状态的一种方式。在我们的案例中，我们在[预览文档](https://github.com/CircleCI-Public/config-preview-sdk/)中对文档做了类似的处理。我们的 preview SDK 至少是从另外两个 repos 发展而来的，被设计成一个地方来绘制我们内部使用的具体代码和伪文档。我们把它竖起来，让潜在客户阅读，就好像它是一个工作产品的文档，然后我们才把它投入使用。这意味着我们可以从一些早期采用者那里获得稳定的反馈，了解我们是否在正确的轨道上。当我们去预览发布时，我们的文档已经足够丰富，从开发到生产的过渡相对“便宜”。

### 在市场发布之前，增量、安静的发布是至关重要的。

在 orbs 正式发布之前，许多用户可以尝试不同版本的 orbs。在我们的营销发布前一个月，我们的功能已经完成，并悄悄地邀请我们的合作伙伴和客户使用它们。在发布之前留出时间，让团队可以进行几波审查、修复 bug、技术债务以及与其他团队的协调，这被证明是相当稳定的发布所必需的。

拥有一个小而活跃的用户群的价值真的不能被夸大。我们很幸运能够与我们的一些客户接触，而不必保密。我们能够限制每个阶段的风险范围，从验证概念到具体的语法决策。我们能够在大范围发布之前解决一些关键的操作和逻辑错误。我们能够在受控但真实的使用模式下安装我们的监控系统并设置我们的运营手册，然后在我们的营销发布后经历流量高峰。

### 有些想法需要很长时间才能变成现实。

球体的想法花了很长时间才最终获得批准。可重用配置组件的最初概念可以追溯到几年前，可以追溯到我们的创始人 Paul Biggar 在 2015 年(orbs 推出前 3 年)所做的设计工作。这个概念在得到产品工程团队的热切关注之前，是断断续续发展起来的。即使在它被首次提出后，也花了几个月的时间让每个人都适应这个概念。最终，这个几乎被遗忘的想法变成了我们的“下一步”计划，因为星星围绕着我们的软件成熟度、我们的中期业务需求和各种客户请求的时间排列。

### 跨组织协调工作应尽早开始。

一次成功的发布有许多部分来自工程之外的部门，所有这些都需要不小的准备时间。我们通常的做法是在项目开始时，而不是结束时，与我们的 SRE、安全、文档、营销和解决方案部门进行基本的情况介绍。特别是对于此次发布，它还包括对我们新的[代码共享服务条款](https://circleci.com/legal/code-sharing-terms/)的法律帮助、对 orb 发布/导入模型的安全审查、文档、连接分析、与营销部门协调以及建立生产就绪运营状态，这些都是发布计划中必须考虑的部分。每一个跨团队的流程都要花费数周的时间才能完成，所以如果我们希望如期完成，提前做好计划是非常重要的。

* * *

在 CircleCI，我们对软件团队的实践进行了大量的思考，同时，我们也在不断地管理我们自己不断增长的团队和雄心。虽然上面的追溯文档要长得多，但我已经分享了包含一般经验的部分，希望对您的团队有价值。

我们喜欢听到团队所依赖的实践和技术来持续地发布高质量的软件产品，我们也喜欢听到你的意见！把你的故事和教训发推特给我们。