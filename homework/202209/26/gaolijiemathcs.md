### 触发器和存储过程的区别是什么？

#### 触发器

触发器trigger是一个特殊的存储过程，执行不是通过程序调用，也不是手工启动，而是由某个事件来触发，例如当对一个表进行操作（insert/delete/update)就会激活，触发器经常用于加强数据库的完整性的规则。

作用：

1.写入数据表之前，强制进行检验或者转换数据。

2.触发器发生错误，异动的结果会被撤销。

#### 存储过程

存储过程：将常用或者很复杂的工作，预先用SQL语句写好并用一个指定的名称存储起来，后面要叫数据库提供与自己定义好的存储过程的功能相同的服务的时候，只需要调用execute，就可以自动完成命令。

存储过程的优点：

1.存储过程只在创造时进行编译，以后每次执行存储的过程不需要重新编译，而SQL语句每执行一次就要编译一次，使用存储过程可以提高执行速度。

2.复杂操作，可以将存储过程封装起来，与数据库提供的事务处理结合在一起使用。

3.存储过程可以重复使用，减少数据库开发人员的工作量。

4.安全性高，可以设定只有某些用户才有对指定存储过程的使用权。



区别：

（1）存储过程为一组已春节并存储在数据库中的SQL语句，可以重用代码。触发器是一种不是由用户直接调用存储的过程，创建触发器会针对特定表或者列的特定类型数据修改时触发。

（2）用户可以使用Execute或者Exec语句来直接调用存储过程，无法直接调用或执行触发器。触发相关事件时，才会自动执行触发器。

（3）存储过程可以采用输入参数，而触发器中不能将参数作为输入传递给触发器。

（4）存储过程可以返回0或n值，触发器无法返回值。

（5）在存储过程中使用事务，触发器内不允许进行事务处理。

（6）存储过程中通常用于执行用户指定的任务，触发器通常用于审计。



ref:

https://www.cnblogs.com/renjiaqi/p/6206373.html

https://blog.csdn.net/yesirwu/article/details/96900005