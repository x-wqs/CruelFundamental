### Linux 如何知晓 OOM？

当程序申请操作系统分配内存时，需要的内存数量会被传递给  vm_enough_memory() ，除非系统管理员设置了内存过载使用，否则 Linux 会检查可用内存是否充足。
Linux 检查可用内存时，除了当前可以直接使用的  free pages  内存，还会检查  page cache  等容易被回收的内存和 swap 交换区的可用空间。
如果这些内存空间加起来能够满足申请分配的数量，Linux 会执行回收并分配内存的动作，不会触发 OOM 处理；否则产生 OOM
