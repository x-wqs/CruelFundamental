### 什么是 Linux 中的文件描述符？dup 系统调用的作用是什么？dup 和 dup2 的区别是什么？

Linux 有一切皆文件的概念，我的理解就是操作系统对大多数调用都用了同一种接口，文件描述符就是要传入的操作对象，这样就能统一接口，实现细节留在操作系统内部。
关于 dup 函数，当我们调用它的时候，dup 会返回一个新的描述符，这个描述一定是当前可用文件描述符中的最小值。我们知道，一般的 0，1，2 描述符分别被标准输入、输出、错误占用，所以在程序中如果 close 掉标准输出 1 后，调用 dup 函数，此时返回的描述符就是 1。
对于 dup2，可以用 fd2 指定新描述符的值，如果 fd2 本身已经打开了，则会先将其关闭。如果 fd 等于 fd2，则返回 fd2，并不关闭它

参考：
https://blog.csdn.net/u012058778/article/details/78705536
https://zhuanlan.zhihu.com/p/105086274
