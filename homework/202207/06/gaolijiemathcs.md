### 什么是共享锁，排他锁，意向锁？

共享锁（读锁/S锁）：多个事务共享一个锁，都可以访问数据，但是其他事务只读不写。

排他锁（写锁/X锁）：多个事务，排他锁同时只能有一个事务获取排他锁，其他事务不能获取其他锁，共享锁和排他锁都不能再删。获取排他锁可以读写数据。

意向锁：InnoDB表级锁

- 意向共享锁（IS）：事务准备给数据加入共享锁，数据行加共享锁需要先获取IS。
- 意向排他锁（IX）：排他锁上锁前加IX。

意向锁由InnoDB自动加。
