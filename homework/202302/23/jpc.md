redis过期删除策略
最初有三种策略
1. 定时删除：在某一时刻遍历所有数据删除所有过期键，比较浪费资源，耗CPU。
2. 惰性删除：在请求访问的时候检查这个key是否过期，如果过期就将其删除。
3. 定期删除：每隔一段时间，随机挑选一些数据进行检查是否过期，如果过期就删除。

redis采用定期删除+惰性删除的策略