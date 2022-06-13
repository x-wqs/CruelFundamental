- OPT: 最佳页面置换算法, 必须知道之后会使用哪些页面. 应该算是理论最优解, 但是实际使用过程中很难提取知道哪些页面会被使用.
- FIFO: 先进先出. 即最先淘汰最早进入队列的, 不过这种方法可能会出现beladey异常现象: 即分配的物理页增多, 缺页概率却增大了. 这种异常可以使用"堆栈型"的LRU算法解决.
- LRU: 最近最少使用. 即先淘汰最近最少使用的, 程序实现的话需要一个哈希和带头尾结点的双链表, 哈希表的值是指向双链表结点的指针.
- LFU: 相比LRU, LFU添加了使用频率信息, 即淘汰使用频率最低的. 如果使用频率相同则淘汰最近最少使用的.
- CLOCK: 时钟页面置换算法.