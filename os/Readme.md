# 操作系统

## 面试问题

## linux

### 进程

- 系统调用流程

> 1.调用c相关函数发起系统调用，将相关参数传入特定寄存器，比如将系统调用编号存入`%eax`中  
> 2.执行中断机器指令`int 0x80`触发软中断，在中断向量表中找到相关中断例程，调用`system_call()`例程  
> 3.根据系统调用编号查询相应系统调用，并执行  

- 进程和线程的区别

> 本质区别: 进程是资源分配的基本单位，线程是cpu调度的基本单位  
> 资源区别: 进程是资源分配的基本单位，但是线程不拥有资源，线程可以访问隶属进程的资源  
> 线程是独立调度的基本单位，在同一进程中，线程的切换不会引起进程切换，从一个进程中的线程切换到另一个进程中的线程时，会引起进程切换
> 系统开销: 由于创建或撤销进程时，系统都要为之分配或回收资源，如内存空间、I/O 设备等，所付出的开销远大于创建或撤销线程时的开销。类似地，在进行进程切换时，涉及当前执行进程 CPU 环境的保存及新调度进程 CPU 环境的设置，而线程切换时只需保存和设置少量寄存器内容，开销很小  
> 通信方面: 线程间可以通过直接读写同一进程中的数据进行通信，但是进程通信需要借助 IPC  

- 进程调度算法
  
> 1.批处理系统: 目标是保证吞吐量和周转时间  
> 1.1 先来先服务器  
> 1.2 短作业优先  
> 1.3 最短剩余时间优先  
> 2.交互式系统: 交互式系统有大量的用户交互操作，在该系统中调度算法的目标是快速地进行响应  
> 2.1 时间片轮转  
> 2.2 优先级调度  
> 2.3 多级反馈队列  
> 3.实时系统: 实时系统要求一个请求在一个确定时间内得到响应  

- 进程通信

> PIPE  
> FIFO 命名管道  
> 共享内存  
> 消息队列  
> 信号  
> socket  

- 共享内存为什么快

> 读取共享内存相当于读取进程自己的虚拟空间, 无需进程上下文切换, 数据也无需再进程中复制

- mmap函数

> mmap()系统调用在调用进程的虚拟地址空间中创建一个新内存映射
>
> 文件映射，匿名映射
>
> **私有文件映射**：映射的内容被初始化为一个文件区域中的内容。多个映射同一个文件 的进程初始时会共享同样的内存物理分页，但系统使用写时复制技术使得一个进程对 映射所做出的变更对其他进程不可见。这种映射的主要用途是使用一个文件的内容来 初始化一块内存区域。一些常见的例子包括根据二进制可执行文件或共享库文件的相
> 应部分来初始化一个进程的文本和数据段
>
> **私有匿名映射**：每次调用 mmap()创建一个私有匿名映射时都会产生一个新映射，该 映射与同一（或不同）进程创建的其他匿名映射是不同的（即不会共享物理分页）。 尽管子进程会继承其父进程的映射，但写时复制语义确保在 fork()之后父进程和子进 程不会看到其他进程对映射所做出的变更。私有匿名映射的主要用途是为一个进程分
> 配新（用零填充）内存
>
> **共享文件映射**：所有映射一个文件的同一区域的进程会共享同样的内存物理分页，这 些分页的内容将被初始化为该文件区域。对映射内容的修改将直接在文件中进行。这 种映射主要用于两个用途。第一，它允许内存映射 I/O，这表示一个文件会被加载到 进程的虚拟内存中的一个区域中并且对该块内容的变更会自动被写入到这个文件中。 因此，内存映射 I/O为使用 read()和 write()来执行文件 I/O 这种做法提供了一种替代方 案。这种映射的第二种用途是允许无关进程共享一块内容以便以一种类似于 System V共享内存段（第 48 章）的方式来执行（快速）IPC
>
> **共享匿名映射**：与私有匿名映射一样，每次调用 mmap()创建一个共享匿名映射时都 会产生一个新的、与任何其他映射不共享分页的截然不同的映射。这里的差别在于映 射的分页不会被写时复制。这意味着当一个子进程在 fork()之后继承映射时，父进程 和子进程共享同样的 RAM 分页，并且一个进程对映射内容所做出的变更会对其他进 程可见。共享匿名映射允许以一种类似于 System V共享内存段的方式来进行 IPC，但
> 只有相关进程之间才能这么做

- linux系统下进程的信号(signal)处理流程是怎么样的

> [link](https://www.zhihu.com/question/24913599)

### 线程

- 线程同步机制

> 互斥锁
> 条件变量
> 读写锁
> 自旋锁
> 信号量

- 线程如何切换

### I/O

- 同步I/O和异步I/O

> 同步IO：用户进程发出IO调用，去获取IO设备数据，双方的数据要经过内核缓冲区同步，完全准备好后，再复制返回到用户进程。而复制返回到用户进程会导致请求进程阻塞，直到I/O操作完成  
> 异步IO：用户进程发出IO调用，去获取IO设备数据，并不需要同步，内核直接复制到进程，整个过程不导致请求进程阻塞

- 五种I/O模型

> 阻塞I/O：进程发起IO系统调用后，进程被阻塞，转到内核空间处理，整个IO处理完毕后返回进程。操作成功则进程获取到数据  
> 非阻塞I/O：进程发起IO系统调用后，如果内核缓冲区没有数据，需要到IO设备中读取，进程返回一个错误而不会被阻塞；进程发起IO系统调用后，如果内核缓冲区有数据，内核就会把数据返回进程  
> I/O复用模型：多个的进程的IO可以注册到一个复用器（select）上，然后用一个进程调用该select， select会监听所有注册进来的IO  
> 信号驱动IO模型：当进程发起一个IO操作，会向内核注册一个信号处理函数，然后进程返回不阻塞；当内核数据就绪时会发送一个信号给进程，进程便在信号处理函数中调用IO读取数据  
>  当进程发起一个IO操作，进程返回（不阻塞），但也不能返回结果；内核把整个IO处理完后，会通知进程结果。如果IO操作成功则进程直接获取到数据

### 死锁

- 死锁的四个必要条件

> 互斥：每个资源要么已经分配给了一个进程，要么就是可用的。  
> 占有和等待：已经得到了某个资源的进程可以再请求新的资源。  
> 不可抢占：已经分配给一个进程的资源不能强制性地被抢占，它只能被占有它的进程显式地释放。  
> 环路等待：有两个或者两个以上的进程组成一条环路，该环路中的每个进程都在等待下一个进程所占有的资源。  

- 死锁处理方法

> 鸵鸟策略
> 死锁检测与死锁恢复
> 死锁预防
> 死锁避免

### 内存管理

- 虚拟地址的优势

> 读写内存的安全性
> 让每个进程有属于自己的地址空间
> 方便分配和释放内存
> 可以分配大于物理内存的虚拟地址空间大小

- 页面置换算法

> LRU
> NGU
> FIFO
> 时钟算法

- 分页和分段的区别

> 页是信息的物理单位，分页是为实现离散分配方式，以消减内存的外零头，提高内存的利用率。段则是信息的逻辑单位，它含有一组其意义相对完整的信息。分段的目的是为了能更好地满足用户的需要。
> 页的大小固定且由系统决定；而段的长度却不固定，决定于用户所编写的程序。
> 分页的地址空间是一维的，程序员只需利用一个记忆符，即可表示一个地址；而分段的作业地址空间是二维的，程序员在标识一个地址时，既需给出段名，又需给出段内地址

## 参考

- MIT 6.S081 课程
- CSAPP
- Linux/UNIX系统编程手册