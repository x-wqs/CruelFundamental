## TCP为什么是三次握手？

1. 确认双方都可以收发数据：在三次握手的过程中，客户端向服务端发送一个SYN（同步）包，服务端收到后回复一个SYN+ACK（同步和确认）包，客户端再回复一个ACK（确认）包。这样，双方都知道彼此可以收发数据。

2. 防止旧连接的干扰：在客户端发送SYN包后，服务端回复SYN+ACK包后，如果没有收到客户端的确认包，服务端会重发SYN+ACK包。如果之前有一个旧连接在断开时留下了一个未完成的SYN包，那么这个SYN包就会在新连接建立时干扰，造成不必要的延迟。

3. 防止重复连接：如果只使用两次握手，那么一个恶意的攻击者可以伪造一个SYN包，让服务端以为有一个新的连接请求，从而建立一个新的连接。使用三次握手可以防止这种攻击，因为攻击者无法伪造一个完整的三次握手的过程。
