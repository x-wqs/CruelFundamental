# 你知道的中间件有哪些？

## 中间件不同层次作用

经过精心设计，现代业务应用可以在本地或跨云端大规模运行。为了构建这些应用，开发人员需要一种具备统一基础功能的应用环境。中间件正是打造这种环境的关键。

我们可以将这些功能分为四层，外加相应的工具：

### 容器层

中间件的这一层将以统一的方式管理应用生命周期的交付。它提供带有CI/CD的 [DevOps](https://www.redhat.com/zh/topics/devops) 能力、容器管理功能以及服务功能。

### 运行时层

该层包含了自定义代码的执行环境。中间件可以为高度分布式云环境、内存中缓存（用于快速访问数据）和消息传递（用于快速数据传输）提供轻量级运行时和框架。

### 集成层

集成中间件可提供相关服务，以通过消息传递、集成和 API 来连接自定义与购买的应用及 SaaS 资产，从而形成功能正常的系统。此外，它还可以提供内存数据库和数据缓存服务、数据/事件流以及 API管理功能。

### 流程自动化和决策管理层

这是开发中间件的最后一层，旨在强化关键智能，实现优化和自动化，以及加强决策管理。



ref:https://www.redhat.com/zh/topics/middleware/what-is-middleware



常见中间件：

- 消息中间件：ActiveMQ，RabbitMQ，RocketMQ、Kafka
- 缓存中间件：Redis
- 数据库层中间件：Driud

- rpc框架：dubbo等等
