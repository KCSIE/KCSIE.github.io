---
layout: post
title: Concurrency-Mutual Exclusion&Synchronization
date: 2020-10-12 11:35:22 +0800
categories: Study
tags: Theory CPU OperatingSystem
img: https://s1.ax1x.com/2020/10/24/BVnO3t.png
author: KCSIE
describe: 并发-互斥与同步 
---

## Concurrency

#### Meaning

Concurrency is the execution of the multiple instruction sequences at the same time. It happens in the operating system when there are several process threads running in parallel. The running process threads always communicate with each other through shared memory or message passing. Concurrency results in sharing of resources result in problems like deadlocks and resources starvation. It helps in techniques like coordinating execution of processes, memory allocation and execution scheduling for maximizing throughput.

Concurrency arises in three different contexts:

+ Multiple applications
  + Multiprogramming
+ Structured application
  + Some application can be designed as a set of concurrent processes
+ Operating-system structure
  + Operating system is a set of processes or threads

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmSZd0.png" alt="" />

#### Principles of Concurrency

Both interleaved and overlapped processes can be viewed as examples of concurrent processes, they both present the same problems.
The relative speed of execution cannot be predicted. It depends on the following:

+ The activities of other processes
+ The way operating system handles interrupts
+ The scheduling policies of the operating system

#### Difficulties of Concurrency

+ Sharing global resources
  + Sharing of global resources safely is difficult. If two processes both make use of a global variable and both perform read and write on that variable, then the order in which various read and write are executed is critical.
+ Optimal allocation of resources
  + It is difficult for the operating system to manage the allocation of resources optimally.
+ Locating programming errors 
  + It is very difficult to locate a programming error because reports are usually not reproducible.
+ Locking the channel
  + It may be inefficient for the operating system to simply lock the channel and prevents its use by other processes.

####  Advantages of Concurrency

+ Running of multiple applications
  + It enable to run multiple applications at the same time.
+ Better resource utilization
  + It enables that the resources that are unused by one application can be used for other applications.
+ Better average response time  
  + Without concurrency, each application has to be run to completion before the next one can be run.
+ Better performance
  + It enables the better performance by the operating system. When one application uses only the processor and another application uses only the disk drive then the time to run both applications concurrently to completion will be shorter than the time to run each application consecutively.

#### Operating System Concerns

+ Keep track of various processes(through PCB)
+ Allocate and deallocate resources
  + Processor time
  + Memory
  + Files
  + I/O devices
+ Protect data and resources
+ Output of process must be independent of the speed of execution of other concurrent processes

#### Process Interaction

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BepfoV.png" alt="" />

#### Competition Among Processes for Resources

+ Mutual Exclusion
  + Only one program at a time is allowed in its critical section
  + Example only one process at a time is allowed to send command to the printer
+ Deadlock
  + It occurs when two processes are blocked and hence neither can proceed to execute.
+ Starvation
  + It occurs when a process does not obtain service to progress.



## 并发

#### 含义

并发是指多个指令序列同时执行。它发生在操作系统中，当有多个进程线程并行运行时。运行中的进程线程总是通过共享内存或消息传递来相互通信。并发的结果是资源共享导致死锁和资源饥饿等问题。它有助于协调进程的执行、内存分配和执行调度等技术，以实现吞吐量的最大化。

并发产生在三种不同的情况下。

+ 多应用程序
  + 多程序
+ 结构化应用程序
  + 一些应用程序可以设计成一组并发进程
+ 操作系统结构
  + 操作系统是一组进程或线程

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmSeoV.png" alt="" />

#### 并发的原则

交错进程和重叠进程都可以看作是并发进程的例子，它们都存在同样的问题。
执行的相对速度是无法预测的。它取决于以下因素：

+ 其他进程的活动
+ 操作系统处理中断的方式
+ 操作系统的调度策略

#### 并发的问题

+ 共享全局资源
  + 全局资源的安全共享是很困难的。如果两个进程都利用一个全局变量，并且都对该变量进行读写，那么各种读写的执行顺序就很关键。
+ 资源的优化分配
  + 操作系统很难对资源的分配进行优化管理。
+ 定位程序错误
  + 要找到一个程序错误是非常困难的，因为报告通常是不可重复的。
+ 锁定通道
  + 对于操作系统来说，简单地锁定通道并阻止其他进程使用它可能是低效的。

#### 并发的优点

+ 运行多个应用程序
  + 可以同时运行多个应用程序。
+ 更好地利用资源
  + 使得一个应用程序未使用的资源可以用于其他应用程序。
+ 更好的平均响应时间  
  + 如果没有并发性，每个应用程序必须运行完成后才能运行下一个应用程序。
+ 更好的性能
  + 它能使操作系统获得更好的性能。当一个应用程序只使用处理器而另一个应用程序只使用磁盘驱动器时，那么同时运行两个应用程序到完成的时间将比连续运行每个应用程序的时间短。

#### 操作系统的考量

+ 追踪各种流程（通过PCB，一个进程的功能和输出结果必须与执行速度(相对于其他并发进程的执行速度)无关）
+ 分配和重新分配资源
  + 处理器时间
  + 内存
  + 文件
  + I/O设备
+ 保护数据和资源
+ 进程的输出必须独立于其他并发进程的执行速度

#### 进程交互

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BepfoV.png" alt="" />

#### 进程间的资源争用

+ 互斥
  
  + 临界区一次只允许一个程序。
  
  + 例子一次只允许一个进程向打印机发送命令。
  
+ 死锁
  
  + 多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。由于线程被无限期地阻塞，因此程序不可能正常终止
  
+ 饥饿
  
  + 由于别的并发的激活的进程持久占有所需资源,使某个异步进程在可预测的时间内不能被激活。



## Synchronization

#### What's Synchronization

Thread synchronization is defined as a mechanism which ensures that two or more concurrent processes or threads do not simultaneously execute some particular program segment known as critical section. Processes' access to critical section is controlled by using synchronization techniques. When one thread starts executing the critical section (serialized segment of the program) the other thread should wait until the first thread finishes. If proper synchronization techniques are not applied, it may cause a race condition where the values of variables may be unpredictable and vary depending on the timings of context switches of the processes or threads.

Another synchronization requirement which needs to be considered is the order in which particular processes or threads should be executed. 

The following are some classic problems of synchronization:

+ The Producer–Consumer Problem (also called The Bounded Buffer Problem)
+ The Readers–Writers Problem

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmSxX9.jpg" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmSv6J.png" alt="" />



#### Race Condition

A race condition occurs when multiple processes or threads read and write data items so that the final result depends on the order of execution of instructions in the multiple processes or thread. Several processes access and process the manipulations over the same data concurrently, then the outcome depends on the particular order in which the access takes place.

A race condition is a situation that may occur inside a critical section. This happens when the result of multiple thread execution in the critical section differs according to the order in which the threads execute.

Race conditions in critical sections can be avoided if the critical section is treated as an atomic instruction. Also, proper thread synchronization using locks or atomic variables can prevent race conditions.

#### Critical Section

Critical section is a code segment that can be accessed by only one process at a time. Critical section contains shared variables which need to be synchronized to maintain consistency of data variables.

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bev7TK.png" alt="" />

Principle of the critical section:

+ Mutual Exclusion : If a process is executing in its critical section, then no other process is allowed to execute in the critical section
+ Progress : If no process is executing in the critical section and other processes are waiting outside the critical section, then only those processes that are not executing in their remainder section can participate in deciding which will enter in the critical section next, and the selection can not be postponed indefinitely
+ Bounded Waiting : A bound must exist on the number of times that other processes are allowed to enter their critical sections after a process has made a request to enter its critical section and before that request is granted

## 同步

#### 什么是同步

线程同步被定义为一种机制，它确保两个或两个以上的并发进程或线程不会同时执行某些特定的程序段，即所谓的临界区。进程对临界区的访问是通过使用同步来控制的。当一个线程开始执行临界区（程序的序列化段）时，另一个线程应该等待，直到第一个线程完成。如果没有采用适当的同步，可能会造成一种竞争条件，即变量的值可能无法预测，并根据进程或线程的上下文切换的时间而变化。

另一个需要考虑的同步要求是特定进程或线程的执行顺序。

以下是同步的一些经典问题：

+ 生产者－消费者问题（也称为边界缓冲区问题）
+ 读者-写者问题

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmSxX9.jpg" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmSv6J.png" alt="" />

#### 竞争条件

竞争条件发生在当多个进程或者线程在读写数据时，其最终结果依赖于多个进程或者线程的指令执行顺序。几个进程同时对同一数据进行访问和处理操作，那么结果就取决于访问的特定顺序。

竞争条件是指在临界区内部可能出现的情况。当临界区中的多个线程执行的结果根据线程执行的顺序不同时，就会出现这种情况。

如果将临界区作为原子指令处理，就可以避免临界区的竞争条件。另外，使用锁或原子变量进行适当的线程同步也可以防止竞争条件的发生。

#### 临界区

临界区是一个代码段，一次只能被一个进程访问。临界区包含共享变量，需要同步以保持数据变量的一致性。

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BevbFO.jpg" alt="" />

临界区原则：

+ 互斥访问：如果一个进程在其关键部分执行，那么其他进程就不允许在关键部分执行
+ 进入：如果没有进程处于临界区内且有进程希望进入临界区, 则只有那些不处于剩余区的进程可以决定哪个进程获得进入临界区的权限，且这个决定不能无限推迟
+ 有限等待：一个进程在提出进入临界区请求后，只需要等待临界区被使用有上限的次数后，该进程就可以进入临界区，即进程不论其优先级多低，不应该在该临界区入口处处于饥饿

## Mutual Exclusion

#### What's Mutual Exclusion

Mutual exclusion is a property of concurrency control, which is instituted for the purpose of preventing race conditions. It is the requirement that one thread of execution never enters its critical section at the same time that another concurrent thread of execution enters its own critical section, which refers to an interval of time during which a thread of execution accesses a shared resource, such as shared memory.

#### Requirements for Mutual Exclusion

1. Only one process at a time is allowed in the critical section for a resource 
2. A process that halts in its noncritical section must do so without interfering with other processes 
3. No deadlock or starvation 
4. A process must not be delayed access to a critical section when there is no other process using it 
5. No assumptions are made about relative process speeds or number of processes 
6. A process remains inside its critical section for a finite time only

#### Enforcing mutual exclusion via hardware

#####  Interrupt Disabling

+ A process runs until it invokes an operating system service or until it is interrupted
+ Disabling interrupts guarantees mutual exclusion on uniprocessor system 
+ Disadvantage:
  + Processor is limited in its ability to interleave programs
  + Disabling interrupts on one processor will not guarantee mutual exclusion in multi-processors environment

```c
while(true){
	//disable interrupts
	//critical section
	//enable interrupts
	//remainder
}
```

##### Compare&Swap (CAS) Instruction

```
int compare_and_swap(int *word, int testval, int newval)
{
    int oldval;
    oldval = *word;
    if(oldval == testval) *word = newval;
    return oldval;
}
```

##### Test&Set (TS) Instruction

```
boolean TestAndSet(boolean *lock){
    boolean old;
    old = *lock;
    *lock=true;
    return old;
}
```

##### Exchange (Swap) Instruction

```
void exchange(int *register, int *memory)
{
    int temp;
    temp = *memory;
    *memory = *register;
    *register = temp;
}
```

##### Using Special Machine Instructions

Advantages:

+ By sharing main memory，it is applicable to any number of processes 
  + single processor
  + multiple processors
+ It is simple and therefore easy to verify
+ It can be used to support multiple critical sections

Disadvantages:

+ Busy-waiting consumes processor time
+ Starvation is possible when a process leaves a critical section and more than one process is waiting.  
+ Deadlock is possible
  + If a low priority process has the critical region and a higher priority process needs, the higher priority process will obtain the processor to wait for the critical region

#### Enforcing mutual exclusion via software

In addition to hardware-supported solutions, some software solutions exist that use busy waiting to achieve mutual exclusion. Including:

+ Dekker's algorithm
+ Peterson's algorithm

##### Dekker's algorithm

Dekker's algorithm allows two threads to share a single-use resource without conflict, using only shared memory for communication.

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm9drd.png" alt="" />

##### Peterson's algorithm

In Peterson’s solution, we have two shared variables:

+ boolean flag[i] :Initialized to FALSE, initially no one is interested in entering the critical section
+ int turn : The process whose turn is to enter the critical section

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm9xd1.png" alt="" />

Peterson’s Solution preserves all three conditions :

+ Mutual Exclusion is assured as only one process can access the critical section at any time
+ Progress is also assured, as a process outside the critical section does not block other processes from entering the critical section
+ Bounded Waiting is preserved as every process gets a fair chance

Disadvantages of Peterson’s Solution

+ It involves Busy waiting
+ It is limited to 2 processes

## 互斥

#### 什么是互斥

互斥是并发控制的一个属性，它是为了防止竞赛条件而设立的。它要求一个执行线程永远不要在另一个并发执行线程进入自己的临界区的时进入它自己的临界区，且 指一个执行线程访问共享资源（如共享内存）的时间间隔。

#### 互斥的要求

1. 一次只允许一个进程进入临界区
2. 忙则等待：阻塞于临界区外的进程不能干涉其它进程
3. 不会发生饥饿和死锁，有限等待
4. 闲则让进：当没有进程在临界区中时，任何需要进入临界区的进程必须能够立即进入
5. 对相关进程的执行速度和处理器数目没有要求
6. 有限占用：一个进程驻留在临界区中的时间必须是有限的

简单来说：

- 空闲让进：当无进程进入临界区时，相应的临界资源处于空闲状态，因而允许一个请求进入临界区的进程立即进入自己的临界区
- 忙则等待：当已有进程进入自己的临界区时，即相应的临界资源正被访问，因而其它试图进入临界区的进程必须等待，以保证进程互斥地访问临界资源
- 有限等待：对要求访问临界资源的进程，应保证进程能在有限时间进入临界区，以免陷入“饥饿”状态
- 让权等待：当进程不能进入自己的临界区时，应立即释放处理机，以免进程陷入忙等

#### 互斥的硬件实现

##### 中断禁用

+ 进程一直运行到调用操作系统服务或被中断为止
+ 禁用中断保证单处理器系统的相互排斥
+ 在某进程开始访问临界区到结束访问为止都不允许中断，也就不能发生进程的切换，因此也不可能发生两个进程同时访问临界区的情况
+ 缺点。
  + 处理器在交错程序方面能力有限
  + 禁用一个处理器上的中断并不能保证多处理器环境下的相互排斥

```c
while (true){    
	//禁用中断    
	//临界区    
	//启用中断    
	//其他部分 
}
```

##### Compare&Swap（CAS） 指令

```
int compare_and_swap(int *word, int testval, int newval)
{
    int oldval;
    oldval = *word;
    if(oldval == testval) *word = newval;
    return oldval;
}
```

##### Test&Set（TS）指令

```
boolean TestAndSet(boolean *lock){
    boolean old;
    old = *lock;
    *lock=true;
    return old;
}
```

##### Exchange（Swap） 指令

```
void exchange(int *register, int *memory)
{
    int temp;
    temp = *memory;
    *memory = *register;
    *register = temp;
}
```

##### 使用特殊的机械指令（原子操作指令锁）

优点:

+ 适用于在单处理器或共享内存的多处理器上的任何数目的进程
+ 非常简单且易于证明
+ 可用于支持多个临界区，每个临界区可以用它自己的变量定义

缺点:

+ 使用了忙等待：当一个进程正在等待进入临界区时，它会继续消耗处理器时间
+ 可能饥饿：当一个进程离开一个临界区并且有多个进程正在等待时，选择哪一个进程是任意的，因此某些进程可能被无限拒绝进入
+ 可能死锁：当某个进程通过专门指令时，在临界区中发生中断将有可能发生死锁

#### 互斥的软件实现

除了硬件支持的解决方案之外，还存在一些使用繁忙等待来实现互斥的软件解决方案。包括：

+ Dekker算法
+ 彼得森算法

##### Dekker算法

Dekker算法允许两个线程共享单次使用的资源而不发生冲突，只使用共享内存进行通信。

##### Peterson算法

在Peterson的解决方案中，我们有两个共享变量：

- boolean flag [i]：初始化为FALSE，最初没有人对进入临界区感兴趣
- int turn：进入关键部分的过程

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmCNF0.jpg" alt="" />

Peterson算法满足解决临界区问题的三个必须标准：互斥访问、进入、有限等待:

+ 互斥是有保证的，因为在任何时候只有一个进程可以访问关键部分
+ 进入也得到保证，因为关键部分之外的进程不会阻止其他进程进入关键部分。
+ 有限等待是满足的因为每个过程都有公平的机会

Peterson算法的缺陷：

+ 它涉及忙等待
+ 只限于2个进程
+ 未遵循让权等待的要求

## Semaphores

#### Overview

Semaphore is simply a variable which is non-negative and shared between threads. This variable is used to solve the critical section problem and to achieve process mutual exclusion&synchronization in the multiprocessing environment.

+ Initialize: May be initialized to a nonnegative number
+ semWait (P)：Wait operation decrements the semaphore value，If the value becomes negative, then the process executing the semWait is blocked
+ semSignal (V)：Signal operation increments semaphore value，If the resulting value is less than or equal to zero, then a process blocked by a semWait operation, if any, is unblocked

Semaphores are of two types:

1. Binary Semaphore – This is also known as mutex lock. It can have only two values – 0 and 1. Its value is initialized to 1. It is used to implement the solution of critical section problem with multiple processes.
2. Counting Semaphore – Its value can range over an unrestricted domain. It is used to control access to a resource that has multiple instances.

Definition of Semaphore Primitives：

```c
typedef struct{
  int value;         
  struct process *L; //queue
} semaphore

void wait(semaphore S) {
  S.value--;
  if(S.value < 0)   //place this process in s.L
      block(S.L);  //block this process
}

void signal(semaphore S) {
  S.value++;
  if(S.value <= 0) //remove a process P from S.L
      wakeup(S.L); //place process P on ready list
}
```

#### Process Synchronization Using Semaphores

Set S as the common semaphores to synchronize processes P1 and P2, with an initial value of 0. The statement y in process P2 is going to use the result of the run of statement x in process P1, so statement y can be executed only when the execution of statement x is complete.

1. Analyze the two operations that need to be synchronized, i.e., the operations that must be guaranteed to execute one before and one after the other sequence
2. Set the sync semaphores S to 0.
3. Execute V(S) after the previous operation
4. Execute P(S) before the post-operation

```c
semaphore S = 0;  //initialize
P1() {
    // …
    x;  
    V(S);  //tell P2, x is done 
}
P2() {
    // …
    P(S);  //check if x is done
    y;  // yes, run y
    // …
}
```

#### Mutual Exclusion Using Semaphores

1. Identify critical section
2. Set the mutual exclusion semaphores (mutex)
3. Execute P(mutex) before the critical section
4. Execute V(mutex) after the critical section

```
semaphore mutex = 1;  //initialize
P1 ( ) {
    // …
    P(mutex);  // ready to visit critical section, lock
    // Process P1's critical section
    V(mutex);  // end, unlock
    // …
}
P2() {
    // …
    P(mutex); //ready to visit critical section, lock
    // Process P2's critical section
    V(mutex);  // end, unlock
    // …
}
```

If there are more than one process in its critical section at a time:

+ Initialize the semaphore to the specified value
+ S.count >= 0: S.count is the number of processes that can execute semWait(s) without suspension
+ S.count < 0: The magnitude of S.count is the number of processes suspended in S.L(queue)

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm2Jk6.png" alt="" />

#### Producer/Consumer Problem

The producer/consumer problem actually contains two main types of threads, a producer thread for producing data, and a consumer thread for consuming data, which is stored uniformly in a shared data area, i.e. , a shared buffer, which should perform the following functions:

+ Blocking the producer from continuing to produce data to be placed in if the buffer is full
+ Blocking consumers from continuing to consume data if the buffer is empty

```c
semaphore mutex=1; //mutex semaphore
semaphore empty=n; //sync semaphore，represent the number of free buffer
semaphore full=0;  //sync semaphore，represent the number of unfree buffer, initialize as empty

producer () 
{
    while(1)
    {
        produce an item in nextp;  
        P(empty);  //get free buffer
        P(mutex);  //enter critical section
        add nextp to buffer; 
        V(mutex);  //leave critical section,release mutex
        V(full);  //the num of full buffer add 1
    }
}

consumer ()
{
    while(1)
    {
        P(full);  //get the num of full buffer add 1
        P(mutex);  //enter critical section
        remove an item from buffer; 
        V (mutex);  //leave critical section,release mutex
        V (empty);  //the num of empty buffer add 1
        consume the item;
    }
}
```

##### Producer/Consumer Problem with Infinite Buffer

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmhLI1.png" alt="" />

```c
producer:
while (true) {
	/* produce item v */
	b[in] = v;
	in++; 
}

consumer:
while (true) {
 	while (in <= out) 
		/*do  nothing */;
	w = b[out];
	out++; 
	/* consume item w */
}
```

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm4Xwj.png" alt="" />

##### Producer/Consumer Problem with Finite Buffer

The buffer is treated as a circular storage, and pointer values must be expressed modulo the size of the buffer.

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm4OmQ.png" alt="" />

The following relationships hold:

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm4jTs.png" alt="" />

```c
producer:
while (true) {
	/* produce item v */
	while ((in + 1) % n == out) 	
		/* do nothing */;
	b[in] = v;
	in = (in + 1) % n
}

consumer:
while (true) {
	while (in == out)
		/* do nothing */;
	w = b[out];
	out = (out + 1) % n;
	/* consume item w */
}
```

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmIAv8.png" alt="" />

#### Difference between Semaphores & Mutex

Strictly speaking, a mutex is locking mechanism used to synchronize access to a resource. Only one task (can be a thread or process based on OS abstraction) can acquire the mutex. It means there is ownership associated with mutex, and only the owner can release the lock (mutex).

Semaphore is signaling mechanism (“I am done, you can carry on” kind of signal). For example, if you are listening songs (assume it as one task) on your mobile and at the same time your friend calls you, an interrupt is triggered upon which an interrupt service routine (ISR) signals the call processing task to wakeup.

Binary semaphore and mutex are not the same because signalling and locking mechanisms are different. The differences between them are in how they are used. While a binary semaphore may be colloquially referred to as a mutex, a true mutex has a more specific use-case and definition, in that only the task that locked the mutex is supposed to unlock it.



## 信号量

#### 概览

信号量简单来说就是一个非负值的变量，在线程之间共享。这个变量用来解决临界区问题，实现多进程下的进程互斥与同步。

+ 初始化：可初始化为一个非负数
+ semWait (P)：P操作使信号量递减，如果信号量的值变为负值，那么执行semWait的进程被阻塞
+ semSignal (V)：V操作使信号量递增，如果递增值小于或等于0，则被P操作阻塞的进程（如果有）将被解除阻塞

信号量有两种类型：

1. 二进制信号量 – 这也被称为互斥锁。它只能有两个值--0和1，其值初始化为1，用于实现多进程的临界区问题的解决。
2. 计数信号量 – 它的值可以在一个非限制的域内（0到一个大于1的限制值）进行。它用于控制对一个有多个实例的资源的访问。

信号量原语定义：

```c
typedef struct{
  int value;         // 剩余资源
  struct process *L;  // 等待队列，当没有资源剩余时，新来的进程将会被放在这个阻塞队列中
} semaphore

/* 某进程需要使用资源时，通过semWait原语申请*/
void semWait(semaphore S) {
  S.value--;
  if(S.value < 0)   // 如果剩余资源不够，使用block原语使进程从运行态进入阻塞态，
      block(S.L);  // 并挂到信号量的等待队列中。
}

/* 进程使用完资源后，通过semSignal原语释放*/
void semSignal(semaphore S) {
  S.value++;
  if(S.value <= 0) // 如果value的值小于0，表示有新的进程在等待资源，所以要唤醒等待队列中的进程
      wakeup(S.L);
}
```

#### 利用信号量实现同步

设S为实现进程P1、P2同步的公共信号量，初值为0。进程P2中的语句y要使用进程P1中语句x的运行结果，所以只有当语句x执行完成之后语句y才可以执行。

1.  分析需要同步的两个操作，即必须保证一前一后的执行顺序的操作
2. 设置同步信号量S，初始为0
3. 在前操作之后执行V(S)
4. 在后操作之前执行P(S)

```c
semaphore S = 0;  //初始化信号量
P1() {
    // …
    x;  //语句x
    V(S);  //告诉进程P2,语句乂已经完成
}
P2() {
    // …
    P(S);  //检查语句x是否运行完成
    y;  // 检查无误，运行y语句
    // …
}
```

#### 利用信号量实现进程互斥

1. 确定临界区
2. 设置互斥信号量（mutex）
3. 在临界区之前执行P(mutex)
4. 在临界区之后执行V(mutex)

```c
semaphore mutex = 1;  //初化信号量
P1 ( ) {
    // …
    P(mutex);  // 准备开始访问临界资源，加锁
    // 进程P1的临界区
    V(mutex);  // 访问结束，解锁
    // …
}
P2() {
    // …
    P(mutex); //准备开始访问临界资源，加锁
    // 进程P2的临界区；
    V(mutex);  // 访问结束，解锁
    // …
}
```

如果在其临界区同时有多个进程:

+ 将信号量初始化为指定的值。
+ S.count >= 0:  S.count是可以不暂停执行semWait(s)的进程数
+ S.count < 0：S.count的大小就是S.L(queue)中暂停的进程数

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm2Jk6.png" alt="" />

#### 生产者/消费者问题

所谓生产者-消费者问题，实际上主要是包含了两类线程，一种是生产者线程用于生产数据，另一种是消费者线程用于消费数据，数据统一存放在一个共享数据区即共享的缓冲区，这个缓冲区应有如下功能：

+ 如果缓冲区已满的话，阻塞生产者继续生产数据放置入内
+ 如果缓冲区为空的话，阻塞消费者继续消费数据

```c
semaphore mutex=1; //临界区互斥信号量，实现对缓冲区的互斥访问
semaphore empty=n; //同步信号量，表示空闲缓冲区数量
semaphore full=0;  //同步信号量，表示非空缓冲区的数量，缓冲区初始化为空

producer ()//生产者进程 
{
    while(1)
    {
        produce an item in nextp;  //生产数据
        P(empty);  //获取空缓冲区单元
        P(mutex);  //进入临界区.
        add nextp to buffer;  //将数据放入缓冲区
        V(mutex);  //离开临界区,释放互斥信号量
        V(full);  //满缓冲区数加1
    }
}

consumer ()//消费者进程
{
    while(1)
    {
        P(full);  //获取满缓冲区单元
        P(mutex);  // 进入临界区
        remove an item from buffer;  //从缓冲区中取出数据
        V (mutex);  //离开临界区，释放互斥信号量
        V (empty);  //空缓冲区数加1
        consume the item;  //消费数据
    }
}
```

##### 无限缓冲区的生产者消费者问题

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmhLI1.png" alt="" />

```c
producer:
while (true) {
	/* 生产物品 v */
	b[in] = v;
	in++; 
}

consumer:
while (true) {
 	while (in <= out) 
		/* 什么都不做 */;
	w = b[out];
	out++; 
	/* 消费物品 w */
}
```

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm4Xwj.png" alt="" />

##### 有限缓冲区的生产者消费者问题

缓冲区被视为一个循环存储，指针值必须以缓冲区的大小为模数来表示。

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm4OmQ.png" alt="" />

有下列关系：

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/Bm4jTs.png" alt="" />

```c
producer:
while (true) {
	/* 生产物品 v */
	while ((in + 1) % n == out) 	
		/* 什么都不做 */;
	b[in] = v;
	in = (in + 1) % n
}

consumer:
while (true) {
	while (in == out)
		/* 什么都不做 */;
	w = b[out];
	out = (out + 1) % n;
	/* 消费物品 w */
}
```

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmIAv8.png" alt="" />

#### 信号量与互斥锁的区别

严格来说，互斥锁是一种锁定机制，用于同步对资源的访问。只有一个任务（可以是基于OS抽象的线程或进程）可以获取互斥量。这意味着存在与互斥锁关联的所有权，并且只有所有者才能释放锁（互斥锁）。

信号量是信号机制（“我做完了，您可以进行”这种信号）。例如，如果您正在手机上收听歌曲（假设它是一项任务），并且您的朋友同时打给您，则会触发中断，中断服务程序（ISR）会在该中断信号通知呼叫处理任务唤醒。

二进制信号量与互斥锁是不同的因为信号机制与锁定机制是不同的。它们的区别在于它们如何被使用。虽然二进制信号量可以通俗地称为互斥锁，但真正的互斥锁有更具体的使用情况和定义，因为只有锁定互斥锁的任务才可以解锁。

## Other

#### Monitors

Monitor is a software module consisting of one ore more procedures, an initialization sequence, and local data.

The chief characteristics are the following:

+ Local data variables are accessible only by the monitor
+ Process enters monitor by invoking one of its procedures
+ Only one process may be executing in the monitor at a time

A monitor supports synchronization by the use of condition variables：

+ cwait(c): Suspend execution of the calling process on condition c. The monitor is now available for use by another process
+ •csignal(c): Resume execution of some process blocked after a cwait on the same condition. If there are several such processes, choose one of them; if there is no such process, do nothing

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmTR3t.png" alt="" />

#### Message Passing

+ Enforce mutual exclusion
+ Exchange information

```c
	send (destination, message)
	receive (source, message)
```

Synchronization：

+ Sender and receiver may or may not be blocking 
+ Blocking send, blocking receive
  + Both sender and receiver are blocked until message is delivered
+ Nonblocking send, blocking receive
  + Sender continues on
  + Receiver is blocked until the requested message arrives
+ Nonblocking send, nonblocking receive
  + Neither party is required to wait

Addressing：

+ Direct addressing
  + Send primitive includes a specific identifier of the destination process
  + Receive primitive could know ahead of time which process a message is expected or receive primitive could use source parameter to return a value when the receive operation has been performed
+ Indirect addressing
  + Messages are sent to a shared data structure consisting of queues
  + Queues are called mailboxes
  + One process sends a message to the mailbox and the other process picks up the message from the mailbox

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmHrYd.png" alt="" />

Message Format：

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmHwwD.png" alt="" />



## 其他

#### 管程

管程由一个或者多个例程、一段初始化代码和局部数据组成。

它的主要特征如下：

+ 局部于管程的数据只能被局部于管程的函数访问
+ 进程调用管程函数进入管程
+ 每次只允许一个进程在管程内执行某个内部过程

管程通过条件变量实现同步：

+ cwait(c)：暂停调用进程在c条件下的执行。 管程现在可供另一个进程使用
+ csignal(c)：恢复在相同条件下进行cwait后受阻的某些进程的执行。如果有几个这样的进程，选择其中一个；如果没有这样的进程，什么也不做

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmTR3t.png" alt="" />

#### 消息传递

+ 实现互斥
+ 交换信息

同步：

+ 发送方和接收方可能会或不会阻塞

+ 阻塞发送，阻塞接收
  + 发件方和收件方都被阻塞直到信息被送达。
+ 非阻塞发送，阻塞接收
  + 发件方继续
  + 接收方被阻塞，直到请求的信息到达。
+ 非阻塞发送，非阻塞接收。
  + 双方都不需要等待

寻址：

+ 直接寻址
    + 发送基元包括目标进程的特定标识符
    + 接收基元可以提前知道预期的消息是哪个进程，或者接收基元可以在执行接收操作时使用源参数返回一个值
+ 间接寻址
  + 消息被发送到一个由队列组成的共享数据结构中
  + 队列被称为邮箱
  + 一个进程向邮箱发送消息，另一个进程从邮箱接收消息

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmHrYd.png" alt="" />

消息格式：

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/25/BmHwwD.png" alt="" />



## Readers/Writers Problem

Having two groups of concurrent processes, reader and writer, sharing a single file, does not produce errors when two or more read processes access the shared data at the same time, but it can lead to data inconsistency errors if a write process and another process (read or write process) access the shared data at the same time. Therefore, there are following requirements：

+ Allows multiple readers to perform read operations on files simultaneously
+ Only one writer is allowed to write a message to the file.
+ No other readers or writers allowed to work until any writer has completed the write operation
+ Before the writer performs the write operation, all existing readers and writers should exit

Mutually Exclusive Relation：

+ Write Process - Write Process
+ Write Process - Read Process

#### Readers Have Priority

When there is a read process, the write operation is delayed, and as long as one read process is active, all subsequent read processes will be allowed to access the file. In this way, the write process may wait for a long time, and there is a "starvation" of the write process.

```c
semaphore write = 1;   //implement writers' mutually exclusive access to files
semaphore mutex = 1;  //guaranteed mutually exclusive access to count variables
int count = 0;   //record the number of currently read processes

writer(){
    while(1){
        P(write);
        //write operation
        V(write);
    }
}

reader(){
    while(1){
		P(mutex);
        if(count == 0)
            P(write);
        count++;
        V(mutex);
        //read operation
        P(mutex);
        count--;
        if(count == 0)
            V(write);
        V(mutex);
    }
}
```

#### Fair Competition

If the write process comes before the read process in order to achieve fair read and write, then the write process has to be executed first. An additional mutually exclusive semaphore can be added.

```c
semaphore write = 1;   //implement writers' mutually exclusive access to files
semaphore read = 1;   //implement fair competition
semaphore mutex = 1;  //guaranteed mutually exclusive access to count variables
int count = 0;   //record the number of currently read processes


writer(){
    while(1){
        P(read);
        P(write);
        //write operation
        V(write);
        V(read);
    }
}

reader(){
    while(1){
        P(read);
		P(mutex);
        if(count == 0)
            P(write);
        count++;
        V(mutex);
        V(read);
        //read operation
        P(mutex);
        count--;
        if(count == 0)
            V(write);
        V(mutex);
    }
}
```

#### Writers Have Priority

Similarly, add a count to the writer

```c
semaphore write = 1;   //implement writers' mutually exclusive access to files
semaphore read = 1;   //writers let readers wait
semaphore rmutex = 1;  //guaranteed mutually exclusive access to rcount variables and avoid the long queue
semaphore wmutex = 1;  //guaranteed mutually exclusive access to rcount variables
int rcount = 0;   //record the number of currently read processes
int wcount = 0;   //record the number of currently write processes

writer(){
    while(1){
        P(wmutex);
        if(wcount == 0)
            p(read);
        wcount++;
        V(wmutex);
        
        P(write);
        //write operation
        V(write);
        
        P(wmutex);
        wcount--;
        if(wcount == 0)
            V(read);
        V(wmutex);
        
    }
}

reader(){
    while(1){
        P(rmutex);     //let the write queue up here, cannot swap places with the following line
        P(read);
        if(count == 0)
            P(write);
        count++;
        V(read);
        V(rmutex);
        //read operation
        P(rmutex);
        count--;
        if(count == 0)
            V(write);
        V(rmutex);
    }
}
```

## 读者写者问题

有读者和写者两组并发进程，共享一个文件，当两个或两个以上的读进程同时访问共享数据时不会产生错误，但是若某个写进程和其他进程（读进程或写进程）同时访问共享数据时则可能导致数据不一致的错误。所以，有如下要求：

+ 允许多个读者可以同时对文件执行读操作
+ 只允许一个写者往文件中写信息
+ 任一写者在完成写操作之前不允许其他读者或写者工作
+ 写者执行写操作前，应让已有的读者和写者全部退出

互斥关系：

+ 写进程-写进程
+ 写进程-读进程

#### 读者优先

当存在读进程时，写操作将被延迟，并且只要有一个读进程活跃，随后而来的读进程都将被允许访问文件。这样的方式下，会导致写进程可能长时间等待，且存在写进程“饿死”的情况。

```c
semaphore write = 1;   //用于实现写者对文件的互斥访问
semaphore mutex = 1;  //用于保证对count变量的互斥访问
int count = 0;   //记录当前读进程的个数

writer(){
    while(1){
        P(write);
        //写操作
        V(write);
    }
}

reader(){
    while(1){
		P(mutex);
        if(count == 0)
            P(write);
        count++;
        V(mutex);
        //读操作
        P(mutex);
        count--;
        if(count == 0)
            V(write);
        V(mutex);
    }
}
```

#### 公平竞争

如果为了实现公平的读写，写进程在读进程之前，那么就要先执行写进程。可以再增加一个互斥信号量。

```c
semaphore write = 1;   //用于实现写者对文件的互斥访问
semaphore read = 1;   //用于实现读写公平
semaphore mutex = 1;  //用于保证对count变量的互斥访问
int count = 0;   //记录当前读进程的个数


writer(){
    while(1){
        P(read);
        P(write);
        //写操作
        V(write);
        V(read);
    }
}

reader(){
    while(1){
        P(read);
		P(mutex);
        if(count == 0)
            P(write);
        count++;
        V(mutex);
        V(read);
        //读操作
        P(mutex);
        count--;
        if(count == 0)
            V(write);
        V(mutex);
    }
}
```

#### 写者优先

类似的，给写者增加一个计数量

```c
semaphore write = 1;   //用于实现写者对文件的互斥访问
semaphore read = 1;   //用于实现写者让读者等待
semaphore rmutex = 1;  //用于保证对rcount变量的互斥访问以及避免长队列
semaphore wmutex = 1;  //用于保证对rcount变量的互斥访问
int rcount = 0;   //记录当前读进程的个数
int wcount = 0;   //记录当前写进程的个数

writer(){
    while(1){
        P(wmutex);
        if(wcount == 0)
            p(read);
        wcount++;
        V(wmutex);
        
        P(write);
        //写操作
        V(write);
        
        P(wmutex);
        wcount--;
        if(wcount == 0)
            V(read);
        V(wmutex);
        
    }
}

reader(){
    while(1){
        P(rmutex);     //让写进程在这里排队，不能与下面一行换位置
        P(read);
        if(count == 0)
            P(write);
        count++;
        V(read);
        V(rmutex);
        //读操作
        P(rmutex);
        count--;
        if(count == 0)
            V(write);
        V(rmutex);
    }
}
```









<img style="display: block; margin: 0 auto;" src="" alt="" />