* 守护进程

守护进程（daemon）是生存期长的一种进程，没有控制终端。它们常常在系统引导装入时启动，仅在系统关闭时才终止。UNIX系统有很多守护进程，守护进程程序的名称通常以字母“d”结尾：例如，syslogd 就是指管理系统日志的守护进程。

* 孤儿进程

一个父进程退出，而它的一个或多个子进程还在运行，那么那些子进程将成为孤儿进程。孤儿进程将被init进程(进程号为1)
所收养，并由init进程对它们完成状态收集工作。由于孤儿进程会被init进程给收养，所以孤儿进程不会对系统造成危害

* 僵尸进程

一个进程使用fork创建子进程，如果子进程退出，而父进程并没有调用wait或waitpid获取子进程的状态信息，那么子进程的进程描述符仍然保存在系统中。这种进程称之为僵死进程。

* 僵死进程的危害

unix提供了一种机制可以保证只要父进程想知道子进程结束时的状态信息， 就可以得到。这种机制就是: 在每个进程退出的时候,内核释放该进程所有的资源,包括打开的文件,占用的内存等。 但是仍然为其保留一定的信息(包括进程号the process
ID,退出状态the termination status of the process,运行时间the amount of CPU time taken by the process等)。直到父进程通过wait /
waitpid来取时才释放。 但这样就导致了问题，如果进程不调用wait / waitpid的话，
那么保留的那段信息就不会释放，其进程号就会一直被占用，但是系统所能使用的进程号是有限的，如果大量的产生僵死进程，将因为没有可用的进程号而导致系统不能产生新的进程. 此即为僵尸进程的危害，应当避免。任何一个子进程(init除外)在exit()
之后，并非马上就消失掉，而是留下一个称为僵尸进程(Zombie)的数据结构，等待父进程处理。这是每个 子进程在结束时都要经过的阶段。如果子进程在exit()
之后，父进程没有来得及处理，这时用ps命令就能看到子进程的状态是“Z”。如果父进程能及时 处理，可能用ps命令就来不及看到子进程的僵尸状态，但这并不等于子进程不经过僵尸状态。
如果父进程在子进程结束之前退出，则子进程将由init接管。init将会以父进程的身份对僵尸状态的子进程进行处理。一个进程如果只复制fork子进程而不负责对子进程进行wait()或是waitpid()
调用来释放其所占有资源的话，那么就会产生很多的僵死进程，如果要消灭系统中大量的僵死进程，只需要将其父进程杀死，此时所有的僵死进程就会编程孤儿进程，从而被init所收养，这样init就会释放所有的僵死进程所占有的资源，从而结束僵死进程。

* 如何避免僵尸进程

程序中显示的调用signal(SIGCHLD, SIG_IGN)来忽略SIGCHLD信号，这样子进程结束后，由内核来wai和释放资源

fork两次，第一次fork的子进程在fork完成后直接退出，这样第二次fork得到的子进程就没有爸爸了，它会自动被老祖宗init收养，init会负责释放它的资源，这样就不会有“僵尸”产生了

对子进程进行wait，释放它们的资源，但是父进程一般没工夫在那里守着，等着子进程的退出，所以，一般使用信号的方式来处理，在收到SIGCHLD信号的时候，在信号处理函数中调用wait操作来释放他们的资源。

[Reference: Zhihu](https://zhuanlan.zhihu.com/p/349109411)
[Reference: Zhihu](https://zhuanlan.zhihu.com/p/263616248)