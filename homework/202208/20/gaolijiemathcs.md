### 硬链接软链接区别？硬中断软中断区别？

硬链接软链接区别？

原理上，硬链接和源文件的inode节点号相同，两者互为硬链接。. 软连接和源文件的inode节点号不同，进而指向的block也不同，软连接block中存放了源文件的路径名。



硬中断软中断区别？

软中断是执行中断指令产生的，而硬中断是由外设引发的 。