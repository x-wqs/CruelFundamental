硬链接和软链接的区别？
- inode：软链接原文件和链接文件拥有不同的inode号，表明是不同的文件，而硬链接和链接文件共用1个inode号，表明是同一个文件。
- 文件属性： 软链接明确写出是链接文件，而硬链接没有写出来，因为本质上硬链接文件和源文件完全平等。
- 软链接支持跨文件系统建立，而硬链接不支持。
- 链接数目： 软链接的链接数目不会增加，文件大小不一样
硬中断和软中断的区别？
- 硬中断： 由硬件产生，例如磁盘，网卡，键盘，时钟等， 处理中断的驱动运行在CPU上，硬中断可以直接中断CPU， 
- 软中断： 由当前正在运行的进程所产生的的，软中断仅与内核联系，软中断不会直接中断cpu:wq
