HTTP/1.0，HTTP/1.1，HTTP/2，HTTP/3的区别

HTTP:
基于TCP协议实现，超文本传输协议
请求-响应协议，指定了客户端可能发送给服务器什么样的消息以及得到什么样的响应
点对点之间通信

HTTP1.0 vs HTTP1.1
长链接
长链接在没有数据通信时，定时发送数据包以维持连接状态

管道
同一个TCP链接中可以同时发出多个请求

断点续传
range字段，用来制定数据字节位置，开启了断点续传的时代

Host头处理
增加了HOST信息

缓存处理
增加了更多的缓存头

错误状态响应码
新增了24个错误状态响应码


HTTP1.1 vs HTTP2
头部压缩
如果发出多个请求并且头部（header）相同，HTTP2会帮你消除同样的部分。（在客户端和服务端维护一张索引表）

二进制格式
HTTP1.1采用明文
HTTP2采用了二进制格式，头信息和数据体都是二进制

数据流
数据包不是按顺序发送的

IO多路复用
可以在一个链接中并发多个请求或回应

服务器推送
服务器可以主动向服务端发送请求


HTTP2 vs HTTP3
协议不同
HTTP2基于TCP
HTTP3基于UDP

QUIC
新增了QUIC协议来实现可靠性的传输

握手次数
HTTP2基于HTTPS，要先进行TCP3次握手，然后进行TLS3次握手，总共6次握手
HTTP3只需要QUIC的3次握手