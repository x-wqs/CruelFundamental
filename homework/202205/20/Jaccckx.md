# TCP的流量控制与堵塞控制



TCP协议作为一个可靠的面向流的传输协议，其可靠性和流量控制由滑动窗口协议保证，而拥塞控制则由控制窗口结合一系列的控制算法实现。滑动窗口协议是一切的基础，以字节流的形式控制流量，将字节序列视为最小单位。一切的流量控制都是建立在滑动窗口协议之上。流量控制是控制发送者与接收者速率匹配问题，而拥塞控制时是避免网络资源被耗尽的问题。流量控制问题相对简单，发送者与接收者在信息交换的过程中，交流接受窗口大小问题。拥塞控制是面向发送者与网络的，接受端用来检查是否掉包，网络过度堵塞即可。



**滑动窗口协议**：

1.  “窗口”对应的是一段可以被发送者发送的字节序列，其连续的范围称之为“窗口”；

2.  “滑动”则是指这段“允许发送的范围”是可以随着发送的过程而变化的，方式就是按顺序“滑动”。

**流量控制**：

​		主要是接收方传递信息给发送方，使其不要发送数据太快，是一种端到端的控制。主要的方式就是返回的ACK中会包含自己的接收窗口的大小，并且利用大小来控制发送方的数据发送。通俗来说就是发送方的发送窗口不能超过接收方给出的接收窗口的数值。

**拥塞控制**：

就是防止过多的数据注入到网络中，这样可以使网络中的路由器或链路不致过载。

常用的方法主要有以下四种：由慢启动开始运行，达到慢启动门限，执行拥塞避免原则，微调数据窗口，并重复执行快重传和快避免。
1). 慢启动：不要一开始就发送大量的数据，先探测一下网络的拥塞程度，也就是说由小到大逐渐增加拥塞窗口的大小；直到发生超时重传，再利用拥塞避免算法和慢启动门限进行一次微调。

2). 拥塞避免：拥塞避免算法让拥塞窗口缓慢增长，即每经过一个往返时间RTT就把发送方的拥塞窗口cwnd加1，而不是加倍，这样拥塞窗口按线性规律缓慢增长。当出现网络拥塞，比如丢包时，将慢开始门限设为原先的一半，然后将cwnd设为1，执行慢启动算法（较低的起点，指数级增长）；

慢启动门限就是说，当拥塞窗口超过门限时，就使用拥塞避免算法，而在门限以内就采用慢启动算法。通常拥塞窗口记做cwnd，慢启动门限记做ssthresh。
![在这里插入图片描述](https://codeantenna.com/image/https://img-blog.csdnimg.cn/20210116094631176.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ppbmdsaTQ1Ng==,size_16,color_FFFFFF,t_70#pic_center)

慢开始和拥塞控制算法常常作为一个整体使用，而快重传和快恢复则是为了减少因为拥塞导致的数据包丢失带来的重传时间，从而避免传递无用的数据到网络。
3). 快重传：
　　1.接收方如果发现一个包丢失，则对后续的包继续发送针对该包的重传请求（为的是使发送方及早知道有报文段没有到达对方）；
　　2. 一旦发送方接收到三个一样的确认，就知道该包之后出现了错误，立刻重传该包，而不必继续等待设置的重传计时器时间到期。；
　　3. 此时发送方开始执行“快恢复”算法：

![在这里插入图片描述](https://codeantenna.com/image/https://img-blog.csdnimg.cn/20210116101946763.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ppbmdsaTQ1Ng==,size_16,color_FFFFFF,t_70#pic_center)

4). 快恢复：快重传配合使用的还有快恢复算法，当发送方连续收到三个重复确认时，就执行“乘法减小”算法，把ssthresh门限减半，但是接下去并不执行慢开始算法：因为如果网络出现拥塞的话就不会收到好几个重复的确认，所以发送方现在认为网络可能没有出现拥塞。所以此时不执行慢开始算法，而是将cwnd设置为ssthresh的大小，然后执行拥塞避免算法。
![在这里插入图片描述](https://codeantenna.com/image/https://img-blog.csdnimg.cn/20210116102719379.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ppbmdsaTQ1Ng==,size_16,color_FFFFFF,t_70#pic_center)