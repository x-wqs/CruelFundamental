# TCP最后一次ACK包没有送到就开始传输数据包，会发生什么？

服务端发送ACK确认包并将自己的seq带入该包, 如果此时服务端没有收到确认就接收到了客户端传输来的数据包, 那么服务端就会发送RST包, 用来关闭异常连接. 

RST包用来关闭异常连接, 不必等待对方的ack确认.