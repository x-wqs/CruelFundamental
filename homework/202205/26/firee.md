### 简述进程调度算法



##### 1.先来先服务调度算法

先来先服务

##### 2.最短作业优先算法

最短作业优先

##### 3.最高响应比优先算法

综合考虑其周转时长和作业用时来分配，避免饿死(ps:如果有饿死现象发生，那肯定是计算资源不足以支撑所有任务，就算不饿死，整个系统的周转时间也会变长)

##### 4.时间片轮转算法

每个进程运行一小段时间



因为进程调度算法由操作系统实现和使用，所以用户级的协程有时候会更适合用户的场景。