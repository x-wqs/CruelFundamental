流量控制是一种机制，用于在发送端和接收端之间限制数据流量的速率，以确保接收方能够及时处理接收到的数据。
在 QUIC 中，每个数据流都有自己的流量控制窗口，它限制了发送方向该流发送的数据量。如果接收方无法及时处理接收到的数据，它可以通过发送 WINDOW_UPDATE 帧来扩大流量控制窗口。

拥塞控制是一种机制，用于避免网络拥塞并保持网络传输的稳定性。
在 QUIC 中，拥塞控制基于 TCP 拥塞控制算法（TCP Congestion Control Algorithm）的思想，即动态调整数据传输速率，以避免网络拥塞。QUIC 使用拥塞窗口（Congestion Window）来控制发送数据的速率。如果发送方检测到网络拥塞，它将减小拥塞窗口，并相应地降低发送速率，以避免进一步加剧网络拥塞。如果发送方检测到网络没有拥塞，它将逐渐增大拥塞窗口，以提高发送速率。

