### 最终一致性，强一致性，弱一致性的区别？

#### 强一致性

系统中的某个数据被成功更新后，后续任何对该数据的读取操作都将得到更新后的值；任何一次读都能读到某个数据的最近一次写的数据。系统中的所有进程，看到的操作顺序，都和全局时钟下的顺序一致。

- 一个集群需要对外部提供强一致性，所以只要集群内部某一台服务器的数据发生了改变，那么就需要等待集群内其他服务器的数据同步完成后，才能正常的对外提供服务。
- 保证了强一致性，务必会损耗可用性。



#### 弱一致性

系统中的某个数据被更新后，后续对该数据的读取操作可能得到更新后的值，也可能是更改前的值。

数据更新后，如果能容忍后续的访问只能访问到部分或者全部访问不到，则是弱一致性。



#### 最终一致性

是弱一致性的特殊形式，存储系统保证在没有新的更新的条件下，最终所有的访问都是最后更新的值。

不保证在任意时刻任意节点上的同一份数据都是相同的，但是随着时间的迁移，不同节点上的同一份数据总是在向趋同的方向变化。

简单说，就是在一段时间后，节点间的数据会最终达到一致状态。



ref:https://blog.csdn.net/Soinice/article/details/97614793
