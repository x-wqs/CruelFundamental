# 简述DNS协议
DNS协议是实现域名和ip地址相互映射的系统，用户可以仅靠记住有实际意义的域名（如google.com）就能访问指定服务，而不是去记冗长无意义的ip地址。从域名到ip地址的映射叫做域名解析。DNS协议运行于UDP之上，使用端口53。

# 简述DNS解析过程
分为两步：
    1.客户机到本地DNS服务器，递归查询：本地客户机发起请求，若本地DNS有缓存目标则直接返回；没有缓存则以本地DNS为递归起点不断查询DNS系统中各个具有上下级关系的DNS服务器，在此期间客户机一直等待。
    2.本地DNS服务器和其他DNS服务器，迭代查询：DNS服务器A对DNS服务器Aa发起请求，若找到结果则返回到递归上一层；若找不到结果，Aa会返回一个指向下一个可用的DNS服务器Ab的指针，让A下次向Ab发起请求。