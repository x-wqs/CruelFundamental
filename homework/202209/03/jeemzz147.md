### 什么是 Linux 中的文件描述符？dup 系统调用的作用是什么？dup 和 dup2 的区别是什么？


内核利用文件描述符来访问文件。文件描述符是非负整数。打开现存文件或新建文件时，内核会返回一个文件描述符。读写文件也需要使用文件描述符来指定待读写的文件。

dup2()与dup()的区别在于可以用newfd来指定新描述符数值，若newfd指向的文件已经被打开，会先将其关闭。若newfd等于oldfd，就不关闭newfd，newfd和oldfd共同指向一份文件。