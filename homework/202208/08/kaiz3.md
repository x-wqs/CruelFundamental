这TIME_WAIT状态的等待时间就是为了防止服务端没有收到客户端发送的第四次挥手的ACK数据包，从而向客户端重新发送第三次挥手的FIN数据包时，客户端能正常接收到FIN数据包并且向服务端发送第四次挥手的ACK应答数据包。

TIME_WAIT状态一般等待的是2MSL的时长。