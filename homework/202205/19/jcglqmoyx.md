CountDownLatch 和 CyclicBarrier 是 Java 并发包提供的两个非常易用的线程同步工具类，把它们放在一起介绍是因为它们之间有点像，又很不同。 CountDownLatch
主要用来解决一个线程等待多个线程的场景，可以类比旅游团团长要等待所有的游客到齐才能去下一个景点。 CyclicBarrier 是一组线程之间互相等待，只要有一个线程没有完成，其他线程都要等待。
对于CountDownLatch来说，重点是那一个线程, 是它在等待，而另外那N个线程在把“某个事情”做完之后可以继续等待，可以终止。 而对于CyclicBarrier来说，重点是那一组（N个)
线程，他们之间任何一个没有完成，所有的线程都必须等待。 除此之外 CountDownLatch 的计数器是不能循环利用的，也就是说一旦计数器减到 0，再有线程调用 await()，该线程会直接通过。 但CyclicBarrier
的计数器是可以循环利用的，而且具备自动重置的功能，一旦计数器减到 0 会自动重置到你设置的初始值。除此之外，CyclicBarrier 还可以设置回调函数，可以说是功能丰富。

[reference](https://juejin.cn/post/6911572211509755912)