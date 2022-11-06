## Windows IOCP

### 什么是IOCP

IOCP全称是I/O Completion Port, 中文翻译为 `I/O 完成端口`, IOCP是一个`异步`的Windows API, 是Windows平台效率最高, 扩展性最好的IO模型, 针对WinSock的海量连接时, 更能显示出威力, 可以高效的将I/O事件通知给应用程序

IOCP模型属于一种`通讯模型`, 适用于WIndows平台下高负载服务器的一个技术, 基于IOCP的开发是异步IO的, 这决定了IOCP所实现的服务器的高吞吐量

完成端口实际上是一个`通知队列`, 由操作系统把已经完成的重叠I/O请求的通知放入其中, 当某项I/O操作一旦完成, 某个可以对该操作结果进行处理的工作线程就会收到一项通知, 而套接字在被创建后, 可以在任何时候与某个完成端口进行关联

### 为什么使用IOCP

在传统模型中, 会出现一个客户端一个线程的问题, 如果软件不是运行在一个多核的情况下, 性能会急剧下降, 线程是系统资源, 并不是无限制的, 也不是低价低廉的

IOCP提供了一种只使用一些(I/O worker)线程去 相对公平的完成多客户端的 输入输出, 如果线程没事干的时候会一直被挂起, 而不会使用CPU时间片, 直到做完为止

### 如何工作

1. 创建一个完成端口(通知队列)
2. 根据CPU个数*2创建Worker线程
3. 创建监听SOCKET, 把socket和完成端口关联起来, 然后开始在指定的端口上监听连接请求
4. 在这个监听Socket上投递AcceptEx请求
5. Worker线程处理的事情
   - 使用GetQueuedCompletionStatus(阻塞函数)扫描完成端口里是否有网络请求的存在, 有就拿出来处理
   - 处理完成再向完成端口投递完成状态



### IOCP 与 epoll

1. Epoll是Linux系统下的模型, IOCP是Windows下的模型
2. Epoll是当事件资源满足发送可处理的通知消息, IOCP是当事件完成时发出完成通知消息
3. Epoll是同步非阻塞, IOCP是异步操作



有一个打印店，有一台打印机，好几个人在排队打印。

普通打印店，正常情况是：

1、你准备好你的文档，来到打印店;

2、排队，等别人打印完;

3、轮到你了，打印你的文档;

4、你取走文档，做后面的处理。

这种方式，你会浪费很多等待时间，非常低效。

于是, Linux和windows都提出了自己最优的模型。

Linux的epoll模型，则可以描述如下：

1、你准备好你的文档，来到打印店;

2、告诉店小二说，我先排队在这位置，轮到我了通知一声(假定你来回路上不耗时);

3、你先去忙你的事情去了;

4、轮到你了，店小二通知你(假定你来回路上不耗时);

5、你获得打印机使用权了，开始打印;

6、打印完了拿走。

你会发现，你节省了排队的时间，等到你能获得打印机资源的时候，告诉你来处理。但是这里，就浪费了一点时间，就是你自己打印。这就是epoll的同步非阻塞。

windows的IOCP模型，则可以描述如下：

1、你准备好你的文档，来到打印店;

2、告诉店小二说，我先排队，轮到我了帮打印下，好了通知我(也假定你来回路上不耗时);

3、你先去忙你的事情去了;

4、轮到你的文档了，店小二直接帮你打印好了，通知你;

5、你来了,直接取走文档。

你会发现，你不但节省了排队时间，你连打印时间都节省了, 完全异步操作。

很显然，IOCP简直是太完美了，可以称得上是最高性能的服务器网络模型了。





那么epoll，kqueue为什么比select和poll高级呢？ 下面我们来分析一下：

首先他们都属于IO复用模型，I/O多路复用模型就是通过一种机制，一个进程可以监视多个描述符，一旦某个描述符就绪（一般是读就绪或者写就绪），能够通知程序进行相应的读写操作。

select主要缺陷是，对单个进程打开的文件描述是有一定限制的，它由FD_SETSIZE设置，默认值是1024，虽然可以通过编译内核改变，但相对麻烦，另外在检查数组中是否有文件描述需要读写时，采用的是线性扫描的方法，即不管这些socket是不是活跃的，我都轮询一遍，所以效率比较低。

poll本质和select没有区别，但其采用链表存储，解决了select最大连接数存在限制的问题，但其也是采用遍历的方式来判断是否有设备就绪，所以效率比较低，另外一个问题是大量的fd数组在用户空间和内核空间之间来回复制传递，也浪费了不少性能。

epoll和kqueue是更先进的IO复用模型，其也没有最大连接数的限制(1G内存，可以打开约10万左右的连接)，并且仅仅使用一个文件描述符，就可以管理多个文件描述符，并且将用户关系的文件描述符的事件存放到内核的一个事件表中（底层采用的是mmap的方式），这样在用户空间和内核空间的copy只需一次。另外这种模型里面，采用了类似事件驱动的回调机制或者叫通知机制，在注册fd时加入特定的状态，一旦fd就绪就会主动通知内核。这样以来就避免了前面说的无脑遍历socket的方法，这种模式下仅仅是活跃的socket连接才会主动通知内核，所以直接将时间复杂度降为O(1)。

最后来聊聊windows的iocp的异步IO模型，目前很少有支持asynchronous I/O的系统，即使windows上的iocp非常出色，但由于其系统本身的局限性和微软的之前的闭源策略，导致主流市场大部分用的还是unix系统，与mac系统的kqueue和linux系统的epoll相比，iocp做到了真正的纯异步io的概念，即在io操作的第二阶段也不阻塞应用程序，但性能好坏，其实取决于copy数据的大小，如果数据包本来就很小，其实这种优化无足轻重，而kqueue与epoll已经做得很优秀了，所以这可能也是unix或者mac系统至今都没有实现纯异步的io模型主要原因。

### IO设计模式

从上面的几种io机制可以看出来，不同的平台实现的io模型可能都不一样，实际上不管哪一种模型，这中间都可以抽象一层API出来，提供一致的接口，目的是为了更好的支持跨平台编程语言的调用，屏蔽操作系统的差异性。这其中广为人知的有C++的ACE,Libevent这些，他们都是跨平台的，而且他们自动选择最优的I/O复用机制，用户只需调用接口即可。IO模型的抽象，总得来说有两种设计模式，分别是Reactor and Proactor模式，这个我们在下篇文章里面专门讨论，这里不在细说。在Java里面，io版本经历了bio，nio，aio的演变，这个我在上篇文章已经介绍过，其实对应io模型，分别是阻塞io，非阻塞io，异步io，这里需要注意的是异步io仅仅在windows上支持，在linux上还是基于epoll的实现的，并非纯异步。