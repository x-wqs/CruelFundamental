**管道（PIPE）**
 管道通信方式的中间介质是文件，通常称这种文件为管道文件。两个进程利用管道文件进行通信时，一个进程为写进程，另一个进程为读进程。写进程通过写端（发送端）往管道文件中写入信息；读进程通过读端（接收端）从管道文件中读取信息。两个进程协调不断地进行写、读，便会构成双方通过管道传递信息的流水线。

消息队列与命名管道类似，但少了打开和关闭管道方面的复杂性。使用消息队列并未解决我们在使用命名管道时遇到的一些问题，如管道满时的阻塞问题。消息队列提供了一种在两个不相关进程间传递数据的简单有效的方法。与命名管道相比：消息队列的优势在于，它独立于发送和接收进程而存在，这消除了在同步命名管道的打开和关闭时可能产生的一些困难。消息队列提供了一种从一个进程向另一个进程发送一个数据块的方法。而且，每个数据块被认为含有一个类型，接收进程可以独立地接收含有不同类型值的数据块。

优点：
 A. 我们可以通过发送消息来几乎完全避免命名管道的同步和阻塞问题。
 B. 我们可以用一些方法来提前查看紧急消息。

缺点：
 A. 与管道一样，每个数据块有一个最大长度的限制。
 B. 系统中所有队列所包含的全部数据块的总长度也有一个上限。

Linux系统中有两个宏定义:
 MSGMAX, 以字节为单位，定义了一条消息的最大长度。
 MSGMNB, 以字节为单位，定义了一个队列的最大长度。

限制：
 由于消息缓冲机制中所使用的缓冲区为共用缓冲区，因此使用消息缓冲机制传送数据时，两通信进程必须满足如下条件。
 （1）在发送进程把写入消息的缓冲区挂入消息队列时，应禁止其他进程对消息队列的访问，否则，将引起消息队列的混乱。同理，当接收进程正从消息队列中取消息时，也应禁止其他进程对该队列的访问。
 （2）当缓冲区中无消息存在时，接收进程不能接收任何消息；而发送进程是否可以发送消息，则只由发送进程是否能够申请缓冲区决定。






