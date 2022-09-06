## 2022/09/03

### 什么是Linux中的文件描述符？dup系统调用的作用是什么？dup和dup2的区别是什么？】



#### 文件描述符

linux会给每个文件分配一个整数ID，这个就是文件描述符`File Descriptor`

- 同一个进程的不同文件描述符可以指向同一个文件
- 不同进程可以拥有相同的文件描述符
- 不同进程的同一个文件描述符可以指向不同的文件
- 不同进程的不同文件描述符也可以指向同一个文件



#### dup

“复制”一个打开的文件号，使两个文件号都指向同一个文件



#### dup和dup2的区别

dup和dup2的区别就是可以用newfd参数指定新描述符的数值，如果newfd已经打开，则先将其关闭，如果newfd等于oldfd，则dup2返回newfd而不关闭它。