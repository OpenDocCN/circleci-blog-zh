# 集成 GitOps 和 DevOps:实现两者的优势

> 原文：<https://circleci.com/blog/gitops-vs-devops/>

GitOps 已经成为一个时髦词。开发人员喜欢它，因为它将 DevOps 折叠到 Git 中，这是一个经常使用和熟悉的工具。使用一个工具来管理多个 DevOps 活动听起来很棒，而且对很多人都有帮助。事实是 GitOps 是有限制的。在本文中，我们将探索 DevOps 和 GitOps，比较它们的相似之处和不同之处，并研究它们的原理如何协同工作来支持您的软件开发目标。

## DevOps 是什么？

DevOps 改变了我们处理和开发软件的方式。这是什么？DevOps 是一套促进开发和运营团队之间协作的工程哲学、工具和文化实践。这种协作减少了团队之间的摩擦，加速了软件开发生命周期，通过更快的反馈实现了更快的软件交付。DevOps 打破了传统软件开发团队中常见的孤岛。

组织经常将开发和操作团队合并成一个单位，在开发过程中一起工作。这个单元通常包含开发生命周期中的每个人，包括质量保证专家和安全分析师。每个人共同努力实现 DevOps 文化。他们实施实践并使用工具，在整个应用生命周期中促进[持续集成和持续交付(CI/CD)](https://circleci.com/blog/what-is-a-ci-cd-pipeline/) 。

这些工具和技术自动化了构建、测试和部署应用程序等过程。作为代码的基础设施是另一个元素，我们将在本文后面讨论。

## 什么是 GitOps？

GitOps 借鉴了 DevOps 的一些思想，将 Git(版本控制系统)和 operations(软件开发的资源管理方面)结合起来。像 DevOps 一样，GitOps 使用基础设施的现有流程作为代码(IaC)、版本控制、代码审查和 CI/CD 管道。

在许多情况下，GitOps 扩展了现有的 DevOps 实践。通过代码部署基础架构消除了团队通常用来设置环境的点击式流程，从而缩短了上市时间。

这种方法还使用合并请求来降低部署糟糕的基础设施的风险。在将更改合并到主分支之前，至少还有一个人会对其进行检查。自动化部署和测试还减少了成本和应用程序停机时间，从而实现了更快的回滚。

### GitOps 在 DevOps 中的传统角色

做得好的话，DevOps 打破了竖井思维，将团队聚集在一起，这样他们可以有效地为共同的目标而工作。GitOps 是 DevOps 的最佳实践，它共享诸如协作、持续改进和自动化等原则。很容易将 GitOps 工作流集成到积极使用的 DevOps 技术中。

许多 DevOps 团队已经在使用 Git 了。毕竟，它是世界上最流行的版本控制系统，GitOps 过程围绕着它。Git 允许团队通过编写声明性代码并将其推送到 repo，频繁而快速地试验新的基础设施和基础设施配置。如果更改破坏了基础设施或者没有按照预期的方式运行，或者如果您对更改不满意，Git history 可以恢复到以前的基础设施版本。

### 使用 GitOps 将基础设施作为代码进行管理

软件应用的进步已经导致许多软件开发过程的自动化。然而，基础设施自动化并没有得到同样的关注。在很大程度上，基础架构的实施和管理仍然是手动过程。像 Ansible 和 Terraform 这样的自动化工具提供了一个良好的开端，但它们不是端到端的解决方案。

IaC 使您能够使用声明性代码来管理和配置基础架构，而不是传统的、耗时的手动过程。与参数化相结合，IaC 允许您使用不同的设置将相同的服务多次部署到不同的环境中。

GitOps 通过充当管理和自动化基础设施的软件开发机制来提供帮助。

## 云原生开发的 GitOps 限制

GitOps 通过简化基础设施部署使软件开发团队受益。尽管 GitOps 的好处很吸引人，但它也有其局限性。GitOps 有几个不足之处:

*   无服务器基础设施
*   机密管理
*   自动化功能

### 无服务器基础设施

采用 GitOps 策略既昂贵又耗时。对于不希望管理部分或全部基础架构的团队来说，无服务器计算成为一种极具吸引力的选择。

无服务器计算提供了一种无需管理基础设施即可部署和执行软件的方式。云提供商会为您解决所有这些问题。

将基础设施管理的任务委托给像 AWS Lambda 或 Azure Functions 这样的云提供商会使 GitOps 过时。开发人员在使用这些功能时，会向云提供商提供一个功能(只是一段代码)。提供者执行该代码。开发人员的组织不需要 GitOps 工具或流程来提供或管理任何基础设施来运行代码。

### 机密管理

应用程序使用秘密进行身份验证和其他敏感的细节。用于连接数据库的字符串是秘密的一个例子。我们必须极其小心地对待这些秘密，以保护我们的软件和系统。

虽然 GitOps 将 Git 放在基础设施管理的中心，但是 Git 并不能帮助管理机密。在公共 Git repo 中保守秘密会使您的应用程序易受攻击。私人回购并没有更安全。所有回购的贡献者都可以看到秘密，这违背了访问管理和基于角色的访问控制(RBAC)的规则。

我们都喜欢 Git 的历史跟踪特性——这是我们使用 Git 的主要原因之一。然而，想想历史跟踪对你的秘密意味着什么。您可能会在某个时候决定从回购中删除这些秘密，但它们将永远存在于 Git 历史中。随着回购数量的增长，每个回购都必须管理自己的秘密。这对管理他们的团队来说是一个挑战。

### 自动化限制

合并和拉取请求的 Git 特性有助于确保我们不会合并和部署糟糕的代码。然而，这是一个需要人工干预的手动过程。它不太符合自动化的理念——这是 GitOps 的一个关键原则。

YAML 文件推动 IaC 部署。GitOps 方法将这些文件存储在 Git 存储库中，并在 YAML 文件发生变化时创建一个合并请求。当流程检查文件并将它们合并到主分支时，它会触发一个部署管道。

随着部署环境数量的增加，这种方法变得更加困难。每个环境都需要一个单独的存储库，因此管理合并请求变得越来越费力。

## 结论

GitOps 补充了现有的 DevOps 战略。使用 Git 这样的版本控制系统来自动化基础设施部署，实验变得更加容易，因为您可以恢复到工作状态。将 GitOps 集成到 DevOps 中很容易，因为它们使用类似的工具集。但是请记住，GitOps 就像任何其他流程一样，并不完美，也有自己的缺陷。

DevOps 和 GitOps 没有内聚性，也不应该紧密耦合。事实上，他们有共同的原则，这意味着他们可以很好地集成在一起，但他们并不需要对方。有 DevOps 文化的团队不需要使用 GitOps——没有 DevOps 文化的团队仍然可以！

实施 DevOps 和 GitOps 战略是一个旅程，CircleCI 可以帮助您和您的团队更快地实现目标。探索 CircleCI 提供的众多 DevOps 工具[来支持您的 DevOps 和 GitOps 工作。](https://circleci.com/)