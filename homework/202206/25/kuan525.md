## C++: new/delete和malloc/free之间有什么关系？

new/delete会调用对象的构造函数/析构函数以完成对象的构造/析构；而malloc则不会。

**new和malloc的区别**

* C与C++动态管理内存的方式不一样，C是使用malloc/free函数，而C++除此之外还有new/delete关键字。
* new/delete是C++关键字，既是运算符也是关键字，需要编译器支持。malloc/free是库函数，需要头文件支持。
* 使用new操作符申请内存分配时无须指定内存块的大小，编译器会根据类型信息自行计算。而malloc则需要显式地指出所需内存的尺寸。
* new操作符内存分配成功时，返回的是对象类型的指针，类型严格与对象匹配，无须进行类型转换，故new是符合类型安全性的操作符。而malloc内存分配成功则是返回void * ，需要通过强制类型转换将void*指针转换成我们需要的类型。
* new内存分配失败时，会抛出bac_alloc异常。malloc分配内存失败时返回NULL。


**总结来说就是，malloc是面向内存的，你要开多大，就给你开多大，开了就不管了。new是面向对象的，根据你指定的数据类型来申请对应的空间，并且能够直接内部调用构造函数生成对象。**

## 使用malloc申请的内存能否通过delete释放？使用new申请的内存能否使用free释放?
**当对象是简单类型时，不会出错，类型过于简单，没有复杂的构造/析构函数，因此此时 new 和 malloc是等价的**

**当对象不是简单类型时：**
1. 使用new申请的内存**不能**否使用free释放？
> 可以，但不安全，通过 free 调用释放 new 申请的内存并不总是能正确的释放所有申请的内存。因为使用 free 方法释放内存时并不会调用实例的析构函数，此时如果实例中有动态申请的内存将因为析构函数没有被调用而没有得到释放，从而导致内存泄漏。而通常你不一定总能知道该类中是否使用了动态内存，因此最佳的做法是 new 与 delete 搭配使用。

2. 使用malloc申请的内存能否通过delete释放？
> 由于malloc没有调用系统的构造函数，由于系统实际分配的空间大于用户程序员所申请的空间（多出来的空间用于记录申请信息和空间进入和离开的标志），在调用delete p的时候，其实仅仅是析构了由申请空间开始的第一段大小为sizeof(T)的空间，所以系统在简单的调用析构函数后，其实没有真正的对后续的内存进行回收，造成了内存泄露.
> 
> 在调用delete []p的时候，系统之前没有在这块内存调用构造函数，所以，delete找不到要释放变量的入口点，之前第一个成功仅仅是单纯的把启始地址当成释放入口点，后面的却找不到了，所以会发生错误。


## delete和delete[]有什么区别？
delete是回收new开辟出的单个对象指针指向的内存。

delete[]是回收new [] 开辟出的对象数组指针指向的内存。

new[]开辟数组空间要多出4个字节来存放数组大小。

delete []要与new []要配套使用，不然会内存泄漏