## TCP拥塞控制，慢启动窗口何时增长，为什么会指数增长？

通常慢启动开始是窗口比较小，小于慢开始门限，因此发送方每发送一个报文，接受方回复一个ACK，发送方将窗口大小增加1，因此，每个轮次中 窗口大小都会翻倍，比如本次窗口是2，需要发送2个报文，每发送一个就增加1个，总共增加两个