# 主从数据库



##### 1.主从数据库的概念

​		主从数据库是一种数据库结构形式，数据库由主库与从库组成。主库对外提供读写操作，从库对外提供读的操作



##### 2.主从数据库的优点

1. 高可用：实时备灾，当主库或从库故障时，可以切换另外一个库

2. 读写分离：减少某个单一库的性能压力

3. 备份数据，避免业务

   

##### 3.数据库主从复制原理

- 主数据库有个bin log二进制文件，记录了所有增删改查SQL语句 （binlog线程）

- 从数据库把主数据库的bin log文件的sql语句复制到自己的中继日志relay log(io线程)
-  从数据库的relay log重做日志文件，再执行一次这些sql语句（sql执行线程）