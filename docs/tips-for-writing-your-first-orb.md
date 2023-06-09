# 编写第一个 orb | CircleCI 的技巧

> 原文：<https://circleci.com/blog/tips-for-writing-your-first-orb/>

在我的上一篇文章中，我回顾了我构建第一个 orb 的过程，并解释了为什么它对于那些想为开源社区做贡献的人来说是一个如此好的选择。在这篇文章中，我想总结一下我在编写 orb 时学到的最重要的东西，给那些想尝试一下的人一些指导(并且[我真的推荐你做](https://circleci.com/blog/how-to-make-an-easy-and-valuable-open-source-contribution-with-circleci-orbs/))！

那么，准备好为那个可爱的开源贡献酱写一个牛逼又受欢迎的 orb 了吗？请记住这些注意事项:

**1。解决问题:**与编程、开发和发明中的任何事情一样，主要目标是解决问题或改善用户体验。有时，这可能仅仅意味着将“这个东西”连接到“那个东西”(更好的说法是集成)。我们的 AWS CLI 和 S3 orb 是将服务实现为 orb 的一个很好的例子。

通过 orbs，您最喜欢的 CLI 工具或 API 可能会变得更容易安装和使用。您甚至可以实现原本不存在的功能(目前还没有！)不带宝珠。

在我的案例中，我们的愿望是提供更加模块化和更好集成的 [Slack 通知](https://circleci.com/developer/orbs/orb/circleci/slack)。我们的许多用户依靠 Slack 通知来接收 CircleCI 上运行的成功或失败的作业的更新，这是一个重要的工具，可以了解是否有任何事情阻碍了您的开发。

**2。给用户自由:**一个伟大的球体的美丽在于简单实用。在创建自己的 orb 时，重要的是要在使工具易于使用和保持足够通用以适应大多数用户需求之间找到平衡。终端用户有一种很好的方式来使用工具和产品，这种方式你可能做梦也想不到。使你的 orb 通用和可扩展意味着它可以为更多的人使用。

再次指向 Slack orb，其中一个参数是发送的消息的颜色。默认情况下，邮件将包含一个灰色的外边框。改变颜色的选项允许用户定制他们的体验:他们可以选择区分不同类型的问题，或者使用不同的颜色来表示不同的项目或团队。这完全取决于用户。

**3。创建一个开发管道:**利用 CircleCI 中的[工作流](https://circleci.com/docs/workflows/)不仅可以像前面提到的那样 lint 和发布 orb，还可以在多个用例场景中测试它。就像任何其他软件一样，我们希望能够在进行变更时[测试我们的代码](https://circleci.com/blog/build-cicd-piplines-using-docker/)——因为变更有时意味着破坏。在启动之前知道您的代码工作正常，这为您提供了创建一个受欢迎的、值得信赖的 orb 的最佳机会，它将为用户提供价值而不会导致任何错误。