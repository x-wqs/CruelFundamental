僵尸进程 / 孤儿进程他们是？区别是啥？
正常情况：父进程创建子进程，子进程再创建新的进程，父子进程异步，父进程无法预测子进程结束。当子进程结束，父进程需要调用wait()或者waitpid()获取子进程终止状态，回收子进程资源。

僵尸进程:父子进程异步执行，父进程没有调用wait函数回收子进程，调用子进程变成僵尸进程占用进程号。僵尸进程被init进程收养后，变成孤儿进程
