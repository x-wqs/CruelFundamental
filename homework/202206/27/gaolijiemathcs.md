### 什么是数据库理论中的CAP原理。 Redis属于根据CAP原理分为的三大类里面的哪一类？ 传统数据库如Mysql属于哪一类？

#### 什么是数据库理论中的CAP原理？

CAP：

- C:Consistency(一致性)：一致性又称为原子性或者事务性。表示一个事务是不可分割的，要不然这个事务完成，要不然这个事务不完成，不会出现完成一半的事务。数据库中脏数据就称为数据没有具有一致性的表现。所有结点在同一时间的数据完全一致。
- A:Availability(可用性)：服务在正常响应时间内一直可用。可用性指系统可以很好的为用户服务，不出现用户操作或者访问超时等用户体验不好的情况。可用性通常情况下可用性和分布式数据冗余，负载均衡等有很大的关联。
- P:Partition Tolerance(分区容错性)：分布式系统在遇到某个结点或者网络分区故障的时候，仍然能够对外提供满足一致性或者可用性的服务。

CAP理论的核心：一个分布式系统不可能同时很好的满足一致性、可用性和分区容错性质，最多只能满足其中两个。

#### Redis属于根据CAP原理分为的三大类里面的哪一类？ 传统数据库如Mysql属于哪一类？

CAP原理，NoSQL数据库分成满足CA原则、CP原则和AP原则三大类。

- CA：单点集群，满足一致性和可用性的系统，通常在可扩展性上不太强大 。（传统数据库，单点MySQL）
- CP：满足一致性，分区容错性的系统，通常性能不是特别高。（Redis、MongoDB）
- AP：满足可用性，分区容错性的系统，通常可能对一致性要求低一些。（大多数网站架构的选择）



ref:https://blog.csdn.net/xiaojin21cen/article/details/81355811

ref:https://zhuanlan.zhihu.com/p/33999708