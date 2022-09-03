### 什么是管道？比进程1写入temp文件和，进程2从temp读取，有什么优点？

#### 什么是管道？

管道是管道是一种半双工的通信方式，数据只能单向流动，而且只能在具有亲缘关系的进程间使用。进程的亲缘关系通常是指父子进程关系。

管道分为无名管道和有名管道，其中无名管道不属于任何文件系统，只存在于内存中，它是无名无形的，但是可以把它看作一种特殊的文件，通过使用普通文件的read(),write()函数对管道进行操作，
有名管道是有名有形的，为了使用这种管道，LINUX中设立了一个专门的特殊文件系统--管道文件，它存在于文件系统中，任何进程可以在任何时候通过有名管道的路径和文件名来访问管道。但是在磁盘上的只是一个节点，而文件的数据则只存在于内存缓冲页面中，与普通管道一样。

#### 与temp文件区别

管道与普通temp文件区别，主要是文件类型和位置可能，管道通信主要通过fd文件，当进程1拿到fd,file,inode操作系统判断这个文件知道是命名管道文件，会在内存中分配内存，操作的时候是在内存中进行操作通信，进程2也打开fd,file,inode，在内存中操作通信。

如果只是用普通的temp文件，可能操作会在磁盘中的文件，效率会比较低。


