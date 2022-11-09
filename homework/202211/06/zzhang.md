Linux 如何知晓 OOM？
　oom_killer（out of memory killer）是Linux内核的一种内存管理机制，在系统可用内存较少的情况下，内核为保证系统还能够继续运行下去，会选择杀掉一些进程释放掉一些内存。通常oom_killer的触发流程是：进程A想要分配物理内存（通常是当进程真正去读写一块内核已经“分配”给它的内存）->触发缺页异常->内核去分配物理内存->物理内存不够了，触发OOM。

　　oom_killer的功能：当系统物理内存不足时，oom_killer遍历当前所有进程，根据进程的内存使用情况进行打分，然后从中选择一个分数最高的进程，杀之取内存。