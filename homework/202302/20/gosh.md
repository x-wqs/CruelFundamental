Redis 如何实现数据不丢失？

数据持久化

RDB
RDB将数据库快照以二进制的方式保存到磁盘中

AOF
AOF以协议文本方式，将所有对数据库进行过写入的命令和参数记录到AOF文件，从而记录数据库状态