Redis 数据类型以及使用场景分别是什么？
Redis的数据类型有string, hash, set, list, zset
string的使用场景主要是用于缓存对象，我们可以使用它来缓存序列化后的对象
hash的使用场景主要是保存结构体，将结构体的成员存入hash中
set主要用于去重，避免用户重复参加活动等
zset可以用于对用户进行去重排名
list可以用于缓存有先后顺序的数据，例如秒杀时用户的先后下单顺序