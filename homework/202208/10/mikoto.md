## epoll的两种触发模式？

- LT水平触发模式    
当被监控的文件描述符上有可读写事件是，epoll会通知程序读写，如果程序没有读写完，那么下次epoll还会通知在未读写完的文件描述符上继续读写

- ET 边缘触发模式    
当被监控的文件描述符上有可读写事件时，epoll通知程序读写，如果数据没有读完，epoll不会继续通知，直到该文件描述符上再次有读写事件
