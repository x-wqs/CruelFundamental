##  什么是RPC框架？
RPC（Remote Procedure Call Protocol）远程过程调用协议，通俗描述是：客户端在不知道调用细节的情况下，调用存在于计算机上的某个远程对象，就像调用本地应用程序一样。
比较正式的描述是：一种通过网络从远程计算机上请求服务，而不需要了解底层网络技术的协议。

### RPC框架的要点：
1. RPC是协议
2. 网络协议和网络IO模型对其透明
3. 信息格式对其透明
4. 应该有跨语言能力

### 为什么要用RPC？
当系统访问量增大，业务增多时，一台单机运行系统的模式已经无法接受，可以将公共业务逻辑抽离出来，独立成service应用，而原有的，新增的应用都可以和独立的service应用交互，以此来完成完整的业务功能。

### 常用RPC框架
1. Thrift
2. gRPC
3. Dubbo
4. Spring Cloud