---
layout: post
title: Processes
date: 2020-09-21 21:48:15 +0800
categories: Study
tags: Theory CPU I/O ComputerScience
img: https://s1.ax1x.com/2020/09/21/wqQkHU.png
author: KCSIE
describe: 进程
---



## Background

#### What's the process?

In computing, a process is the instance of a computer program that is being executed by one or many threads. It contains the program code and its activity. Depending on the operating system (OS), a process may be made up of multiple threads of execution that execute instructions concurrently.

In short, process is:

+ A program in execution

+ An instance of a program running on a computer

+ The entity that can be assigned to and executed on a processor

+ A unit of activity characterized by

  - The execution of a sequence of instructions

  - A current state

  - An associated set of system resources




#### Difference between Program and Process



|                           Program                            |                           Process                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| When we execute a program that was just compiled, the OS will generate a process to execute the program. Execution of the program starts via GUI mouse clicks, command line entry of its name, etc. A program is a passive entity as it resides in the secondary memory, such as the contents of a file stored on disk. One program can have several processes. | The term process (Job) refers to program code that has been loaded into a computer’s memory so that it can be executed by the central processing unit (CPU). A process can be described as an instance of a program running on a computer or as an entity that can be assigned to and executed on a processor. A program becomes a process when loaded into memory and thus is an active entity. |
| Program contains a set of instructions designed to complete a specific task. |       Process is an instance of an executing program.        |
| Program is a passive entity as it resides in the secondary memory. | Process is a active entity as it is created during execution and loaded into the main memory. |
| Program exists at a single place and continues to exist until it is deleted. | Process exists for a limited span of time as it gets terminated after the completion of task. |
|                 Program is a static entity.                  |                 Process is a dynamic entity.                 |
| Program does not have any resource requirement, it only requires memory space for storing the instructions. | Process has a high resource requirement, it needs resources like CPU, memory address, I/O during its lifetime. |
|           Program does not have any control block.           | Process has its own control block called Process Control Block. |



#### Process Control Block

Process control blocks:

+ Contains the process elements

  - Identifier
  - State
  - Priority
  - Program counter
  - Memory pointers
  - Context data
  - I/O status information
  - Accounting information

+ Created and managed by the operating system

+ Allows support for multiple processes

  

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/21/wqNtPK.png" alt="" />



## 背景

#### 什么是进程？

进程是一个或多个线程正在执行的计算机程序的实例。它包含程序代码及其活动。根据操作系统(OS)的不同，一个进程可能由多个并发执行指令的执行线程组成。

简单来说，进程是：

+ 正在执行的程序

+ 计算机上运行的程序的实例

+ 可分配给处理器并在处理器上执行的实体

+  一个有如下活动特点的单位

  - 一系列指令的执行

  - 当前状态

  - 一套相关的系统资源




#### 程序和进程的区别



|                           Program                            |                           Process                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| 当我们执行一个刚刚编译好的程序时，操作系统会生成一个进程来执行程序。程序的执行是通过GUI鼠标点击、命令行输入其名称等方式开始的。一个程序是一个被动的实体，因为它驻留在二级存储器中，如存储在磁盘上的文件内容。一个程序可以有多个进程。 | 术语 "进程"(也叫Job)是指已经加载到计算机内存中的程序代码，以便它可以被中央处理单元(CPU)执行。进程可以被描述为在计算机上运行的程序实例，也可以被描述为可以分配给处理器并在处理器上执行的实体。一个程序在加载到内存中时就成为一个进程，因此是一个活动的实体。 |
|          程序包含一组指令，旨在完成一个特定的任务。          |                  进程是一个执行程序的实例。                  |
|        程序是一个被动实体，因为它驻留在二级存储器中。        | 进程是一个主动实体，因为它是在执行过程中创建并加载到主内存中的。 |
|         程序存在于一个地方，并持续存在，直到被删除。         |       进程存在的时间有限，因为它在任务完成后会被终止。       |
|                        程序是静态的。                        |                        进程是动态的。                        |
|      程序没有任何资源要求，它只需要内存空间来存储指令。      | 进程对资源的要求很高，它在生命周期中需要CPU、内存地址、I/O等资源。 |
|                     程序没有任何控制块。                     |             进程有自己的控制块，称为进程控制块。             |



#### 进程控制块

进程控制块：

+ 包含进程元素
  - 标识符
  - 状态
  - 优先级
  - 程序计数器
  - 内存指针
  - 上下文数据
  - I/O 状态信息
  - 记账信息
+ 由操作系统创建和管理
+ 允许支持多个进程



<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/21/wqaBNt.png" alt="" />



## Process states

An operating system kernel that allows multitasking needs processes to have certain states. Names for these states are not standardised, but they have similar functionality.

+ First, the process is "created" by being loaded from a secondary storage device (hard disk drive, CD-ROM, etc.) into main memory. After that the process scheduler assigns it the "waiting" state.
+ While the process is "waiting", it waits for the scheduler to do a so-called context switch. The context switch loads the process into the processor and changes the state to "running" while the previously "running" process is stored in a "waiting" state.
+ If a process in the "running" state needs to wait for a resource (wait for user input or file to open, for example), it is assigned the "blocked" state. The process state is changed back to "waiting" when the process no longer needs to wait (in a blocked state).
+ Once the process finishes execution, or is terminated by the operating system, it is no longer needed. The process is removed instantly or is moved to the "terminated" state. When removed, it just waits to be removed from main memory.

This is the basic process of the process state. Let's look at the details next.

#### Trace of Process

+ Sequence of instruction that execute for a process

+ Dispatcher switches the processor from one process to another

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PoUbR.png" alt="" />

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0Pol5V.png" alt="" />

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PoQU0.png" alt="" />

#### Two-State Process Model

Process may be in one of two states:

+ Running
+ Not-running

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PHDP0.png" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PH05q.png" alt="" />

Limit of Two-State Process Model:

+ Not-running
  - ready to execute
  - waiting for I/O (blocked)
+ Dispatcher cannot just select the process that has been in the queue the longest because it may be blocked.



#### The Creation and Termination of Processes

Reasons for Process Creation

+ New batch job
+ Interactive log-on
+ Created by OS to provide a service
+ Spawned by existing process

Reasons for Process Termination

+ Normal completion
+ Time limit exceeded
+ Memory unavailable
+ Bounds violation
+ Protection error
+ Arithmetic error
+ Time overrun
+ I/O failure
+ Invalid instruction
+ Privileged instruction
+ Data misuse
+ Operator or OS intervention
+ Parent termination
+ Parent request

#### A Five-State Model

Five States:

+ Running
+ Ready
+ Blocked
+ New
+ Exit

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PvUSI.png" alt="" />

Using Two Queues

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PvtfA.png" alt="" />

Multiple Blocked Queues

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PvI7F.png" alt="" />

#### Suspended Processes

+ Processor is faster than I/O so all processes could be waiting for I/O
+ Swap these processes to disk to free up more memory
+ Blocked state becomes suspend state when swapped to disk
+ Two new states
  - Blocked/Suspend
  - Ready/Suspend

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0iCeYD.png" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0iCmfe.png" alt="" />

Reasons for Process Suspension:

+ Swapping
+ Other OS reason
+ Interactive user request
+ Timing
+ Parent process request



## 进程状态

一个操作系统内核，允许多任务需要进程具有一定的状态。这些状态的名称并不统一，但它们的功能相似。

+ 首先，进程被 "创建"，从二级存储设备（硬盘驱动器、光盘等）加载到主内存中。之后，进程调度器会给它分配 "等待 "状态。
+ 当进程处于 "等待 "状态时，它等待调度器进行所谓的上下文切换。上下文切换将进程加载到处理器中，并将状态改为 "运行"，而之前 "运行 "的进程则存储在 "等待 "状态。
+ 如果一个处于 "运行 "状态的进程需要等待资源（例如等待用户输入或文件打开），它被分配到 "阻塞 "状态。当进程不再需要等待时（在阻塞状态下），进程状态就会变回 "等待"。
+ 进程一旦完成执行，或者被操作系统终止，它就不再需要了。进程会立即被删除，或者被移到 "终止 "状态。删除时，只需等待从主内存中删除即可。

上面是进程状态的基本过程。接下来我们来看看细节。

#### 进程轨迹

+ 进程执行的指令序列
+ 调度器将处理器从一个进程切换到另一个进程

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PT7Y6.jpg" alt="" />

#### 双状态过程模型

进程可能处于两种状态：

+ 运行
+ 不运行

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PqpkR.png" alt="" />

双状态模型的限制：

+ 不运行
  - 准备执行
  - 等待I/O指令（阻塞）
+ 分派器不能只考虑选择队列中最老的进程，相反，它应该扫描这个列表，查找那些未被阻塞且在队列中时间最长的进程。

#### 进程的产生和终止

进程产生的原因：

+ 批处理任务
+ 交互式命令
+ OS创建以提供服务
+ 现有进程（父进程）创建

进程终止的原因：

+ 正常结束
+ 超时限制
+ 内存空间不足
+ 越界
+ 保护错误
+ 算术错误
+ 等待时间超时
+ I/O异常
+ 无效指令
+ 特权指令
+ 错用数据类型（未初始化）
+ OS介入
+ 父进程终止
+ 父进程请求

#### 五状态进程模型

五个状态：

+ 运行态
+ 就绪态
+ 阻塞态
+ 新建态
+ 退出态

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PzOeK.png" alt="" />

使用两个队列（单阻塞队列）类上

多个阻塞队列

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0PvD0S.jpg" alt="" />

#### 被挂起（暂停）的进程

+ 处理器的速度比I/O快，所以所有的进程都可能在等待I/O
+ 将这些进程交换到磁盘，以释放更多的内存
+ 切换到磁盘时，阻塞状态变为挂起状态
+ 两个新状态
  - 阻塞/挂起
  - 准备/挂起

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0iCM6A.jpg" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0iCQOI.png" alt="" />

挂起的原因：

+ 交换
+ 其他OS原因
+ 交互式用户请求
+ 定时
+ 父进程请求



## Process Description

#### Operating System Control Structures

+ Information about the current status of each process and resource 
+ Tables are constructed for each entity the operating system manages 

Structure of OS Control Tables

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0ii2LR.png" alt="" />

Memory Tables:

+ Allocation of main memory to processes 
+ Allocation of secondary memory to processes 
+ Protection attributes for access to shared memory regions
+ Information needed to manage virtual memory

I/O Tables:

+ I/O device is available or assigned
+ Status of I/O operation 
+ Location in main memory being used as the source or destination of the I/O transfer 

File Tables:

+ Existence of files
+ Location on secondary memory
+ Current Status
+ Attributes

Process Table: Every entry is a description of a process image

Process Image: Collection of program, data, stack, attributes

#### Process Control Structures

+ Process Identification

+ Processor State Information
  - User-Visible Registers
  - Control and Status Registers
  - Stack Pointers

+ Process Control information
  - Scheduling and State Information
  - Data Structuring (link information)
  - Interprocess Communication
  - Process Privileges
  - Memory Management
  - Resource Ownership and Utilization





## 进程的描述

#### 操作系统的控制结构

+ 每个进程和资源的当前状态
+ 操作系统构造并维护他所管理的所有实体的信息表

OS控制表结构

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/26/0ikuUP.png" alt="" />

内存表：

+ 分配给进程的主存
+ 分配给进程的辅存
+ 共享内存区域的保护属性
+ 虚拟内存的管理信息

I/O表：

+ I/O 设备处于分配状态
+ I/O 操作的状态
+ 数据传送的源和目的地址

文件表：

+ 文件是否存在
+ 在第二存储器（硬盘）的位置
+ 当前状态
+ 属性

进程表： 每个条目都是一个过程图像的描述

进程图像：程序、数据、栈、属性的集合

#### 进程控制结构

+ 进程识别

+ 处理器状态信息
  - 用户可见的寄存器
  - 控制和状态寄存器
  - 堆栈指针

+ 进程控制信息
  - 时间和状态信息
  - 数据结构信息（可以以队列、环或者别的结构形式与其他进程进行链接）
  - 进程间通信
  - 进程权限
  - 内存管理
  - 资源的所有权和利用情况

## Execution of the Operating System

#### Non-process Kernel

+ Execute kernel outside of any process
+ Operating system code is executed as a separate entity that operates in privileged mode

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CThV.png" alt="" />

#### Execution Within User Processes

+ Operating system software within context of a user process
+ Process executes in privileged mode when executing operating system code

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CHpT.png" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CLX4.png" alt="" />

#### Process-Based Operating System

+ Implement operating system as a collection of system processes
+ Useful in multi-processor or multi-computer environment

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CqcF.png" alt="" />





## 操作系统的执行

#### 无进程内核

+ 在任何进程之外执行内核
+ 操作系统代码作为一个单独的实体，在特权模式下执行

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CThV.png" alt="" />

#### 在用户进程中执行

+ 用户进程中的操作系统软件
+ 执行操作系统代码时，进程在特权模式下执行

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CHpT.png" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CLX4.png" alt="" />

#### 基于进程的OS

+ 将操作系统作为系统进程的集合来实施
+ 在多处理器或多计算机环境中有用

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/10/03/08CqcF.png" alt="" />