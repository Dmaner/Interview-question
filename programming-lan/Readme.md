# 语言

## c++

- 动态连接和静态链接

> 静态链接: 链接阶段，会将汇编生成的目标文件.o与引用到的库一起链接打包到可执行文件中
> 动态链接: 动态库在程序编译时并不会被连接到目标代码中，而是在程序运行是才被载入。不同的应用程序如果调用相同的库，那么在内存里只需要有一份该共享库的实例

- 内存对齐

> 为什么要进行内存对齐: 尽管内存是以字节为单位，但是大部分处理器并不是按字节块来存取内存的.它一般会以双字节,四字节,8字节,16字节甚至32字节为单位来存取内存，我们将上述这些存取单位称为内存存取粒度  

## java

- ArrayList和LinkedList的区别

> 1. ArrayList的实现是基于数组，LinkedList的实现是基于双向链表。
> 2. 对于随机访问，ArrayList优于LinkedList
> 3. 对于插入和删除操作
> 4. LinkedList比ArrayList更占内存，因为LinkedList的节点除了存储数据，还存储了两个引用，一个指向前一个元素，一个指向后一个元素

- 乐观锁&悲观锁

> [链接](https://www.cnblogs.com/kismetv/p/10787228.html)

- volatile有哪些特性？

> volatile实际上是通过读写屏障实现的。读写屏障就有两个作用：缓冲失效和阻止指令重排序

- Java多线程的线程池参数

> corePoolSize：核心线程数，定义了最少可以同时运行的线程数量，当有新的任务时就会创建一个线程执行任务，当线程池中的线程数量达到 corePoolSize 之后，到达的任务进入阻塞队列。
> maximumPoolSize：最大线程数，定义了线程池中最多能创建的线程数量。
> keepAliveTime：等待时间，当线程池中的线程数量大于 corePoolSize 时，如果一个线程的空闲时间达到 keepAliveTime 时则会终止，直到线程池中的线程数不超过 corePoolSize。
> unit：参数 keepAliveTime 的单位。
> workQueue：阻塞队列，用来存储等待执行的任务。
> threadFactory：创建线程的工厂。
> handler：当拒绝处理任务时的策略

- AIO、BIO、NIO的区别

> BIO（同步阻塞I/O模式）
> NIO（同步非阻塞）
> AIO（异步非阻塞I/O模型）