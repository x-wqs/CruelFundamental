### 为什么需要四次挥手？

服务器收到客户端的 FIN 报文时，内核会马上回一个 ACK 应答报文，**但是服务端应用程序可能还有数据要发送，所以并不能马上发送 FIN 报文，而是将发送 FIN 报文的控制权交给服务端应用程序**

没有数据要发送并且开启了 TCP 延迟确认机制，那么第二和第三次挥手就会合并传输，这样就出现了三次挥手。

