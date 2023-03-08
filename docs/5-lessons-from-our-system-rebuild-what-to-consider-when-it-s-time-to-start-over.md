# CircleCI | 5 个重构系统的技巧

> 原文：<https://circleci.com/blog/5-lessons-from-our-system-rebuild-what-to-consider-when-it-s-time-to-start-over/>

两年前，经过快速增长后，我们的基础设施效率接近本地最高水平，但我们知道重新架构有风险。我们绞尽脑汁，寻找一种方法来逐步更新我们的平台，但我们功亏一篑。最终，我们得出了一个令人生畏的结论:我们将不得不踏上一段危险的旅程——对我们的基础设施进行彻底的平台迁移。

因为我们的工具对许多公司来说都是至关重要的，所以我们感到了一种额外的压力，那就是要快速完成我们的重建，并确保它做得很好。在第一个顾客看到我们新系统的任何部分之前的六个月，真是紧张不安。但是，经过仔细的规划、建设、更多的规划和重建，我们终于[出现了](https://circleci.com/blog/why-we-broke-our-philosophical-vows-to-bring-you-circleci-2-0/) -现在有了一个更新的平台，比我们原来的平台性能好得多。当我们在破土动工 9 个月后推出新平台 GA 时，它证实了我们的信念，即我们的新系统更智能、更一致，重新架构是值得的。

回顾过去，我可以看到对我们成功的重新架构至关重要的 5 个重要概念。以下是我学到的:

### 1.在找到适合市场的产品之前，优化速度，而不是优雅。

有一种关于完美架构系统的说法:我们从未听说过它们，因为那些公司从未起步。当您第一次开始时，选择目前有效的堆栈，而不是为未来的可能性过度优化，是正确的选择。

许多初创公司在找到产品市场契合度之前，关注了错误的事情。他们浪费时间谈论他们想要建立的公司，而不是创建一个版本。相反，把你所有的精力都集中在开发产品上，以支持你想在未来扩大规模的公司。一旦你有了这些，你就能找到一条可持续发展的道路。

### 2.基础架构的改变不会逐渐发生。

在你找到适合你的产品市场，并且达到临界质量后，等待太长时间来完善你的基础设施会破坏你的可靠性和发展能力。在 CircleCI，我们感受到了重新设计的日益增长的需求，但我们也感受到了这样做的巨大危险。

重组迫使我们认真审视我们的原则:在 CI/CD 的所有好处中，我们可以在重建中保留什么？我们要扔掉什么？在重写核心产品的同时，我们如何继续在产品的其他领域取得进展？我们本可以固执地坚持渐进式改进。但是相反，我们投入到这个项目中，因为我们知道另一面会是什么:更好的持续交付。

### 3.限制你的范围。

在整个重建过程中，我们尽最大努力缩小关注范围。我们专注于做出我们知道会产生影响的改变，同时尽量减少其他地方的改变。我们还通过分支级别的配置公开了新的流程，因此我们可以在不中断客户日常软件交付的情况下征求真实的反馈。这对我们很重要。我们知道在重建过程中会对客户产生暂时的影响，但我们希望尽可能地减少影响。

### 4.客户反馈是关键。

存在设计缺陷、架构缺陷和决策，这些决策在纸面上是有意义的，但是一旦我们交付了它们，它们就不起作用了。利用客户反馈来帮助我们识别这些缺陷是至关重要的。反馈帮助我们构建了一个更好、更智能的产品，我们非常感谢我们的客户给了我们他们的意见。

当你处于创业阶段，在非常早期的时候，你需要明白你是否在做客户真正想要的、市场会接受的东西。始终认真对待客户的反馈，并始终致力于打造一款为用户和市场增加价值的产品。

### 5.给你的团队一个“完成”的明确定义

不可否认的是，永远继续修补产品是很诱人的，陷入了无休止的完美主义的漩涡。但是我们知道我们需要回到我们的核心理念:不断为我们的客户提供价值。因此，我们承诺将这个升级版本作为我们的默认平台，并在此基础上构建了令人兴奋的功能。

### 结论

在一天结束时，一些风险是必要的，这是其中之一。尽管重新架构是一项极其艰巨的任务，但它帮助我们改善了客户的体验，并为更多的产品创新铺平了道路。如果你觉得是时候重建了，我的最终建议是倾听——倾听你的客户，倾听市场，倾听你为自己设定的目标和界限——在你开始重建的时候，用这些建议来帮助自己走向成功。