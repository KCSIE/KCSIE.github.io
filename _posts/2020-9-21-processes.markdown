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

### What's a process?

In computing, a process is the instance of a computer program that is being executed by one or many threads. It contains the program code and its activity. Depending on the operating system (OS), a process may be made up of multiple threads of execution that execute instructions concurrently.

In short, process is:

+ A program in execution

+ An instance of a program running on a computer

+ The entity that can be assigned to and executed on a processor

+ A unit of activity characterized by

  - The execution of a sequence of instructions

  - A current state

  - An associated set of system resources

    

### Difference between Program and Process



|                           Program                            |                           Process                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| When we execute a program that was just compiled, the OS will generate a process to execute the program. Execution of the program starts via GUI mouse clicks, command line entry of its name, etc. A program is a passive entity as it resides in the secondary memory, such as the contents of a file stored on disk. One program can have several processes. | The term process (Job) refers to program code that has been loaded into a computer’s memory so that it can be executed by the central processing unit (CPU). A process can be described as an instance of a program running on a computer or as an entity that can be assigned to and executed on a processor. A program becomes a process when loaded into memory and thus is an active entity. |
| Program contains a set of instructions designed to complete a specific task. |       Process is an instance of an executing program.        |
| Program is a passive entity as it resides in the secondary memory. | Process is a active entity as it is created during execution and loaded into the main memory. |
| Program exists at a single place and continues to exist until it is deleted. | Process exists for a limited span of time as it gets terminated after the completion of task. |
|                 Program is a static entity.                  |                 Process is a dynamic entity.                 |
| Program does not have any resource requirement, it only requires memory space for storing the instructions. | Process has a high resource requirement, it needs resources like CPU, memory address, I/O during its lifetime. |
|           Program does not have any control block.           | Process has its own control block called Process Control Block. |



### Process Control Block

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

### 什么是进程？

进程是一个或多个线程正在执行的计算机程序的实例。它包含程序代码及其活动。根据操作系统(OS)的不同，一个进程可能由多个并发执行指令的执行线程组成。

简单来说，进程是：

+ 正在执行的程序

+ 计算机上运行的程序的实例

+ 可分配给处理器并在处理器上执行的实体

+  一个有如下活动特点的单位

  - 一系列指令的执行

  - 当前状态

  - 一套相关的系统资源

    

### 程序和进程的区别



|                           Program                            |                           Process                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| 当我们执行一个刚刚编译好的程序时，操作系统会生成一个进程来执行程序。程序的执行是通过GUI鼠标点击、命令行输入其名称等方式开始的。一个程序是一个被动的实体，因为它驻留在二级存储器中，如存储在磁盘上的文件内容。一个程序可以有多个进程。 | 术语 "进程"(也叫Job)是指已经加载到计算机内存中的程序代码，以便它可以被中央处理单元(CPU)执行。进程可以被描述为在计算机上运行的程序实例，也可以被描述为可以分配给处理器并在处理器上执行的实体。一个程序在加载到内存中时就成为一个进程，因此是一个活动的实体。 |
|          程序包含一组指令，旨在完成一个特定的任务。          |                  进程是一个执行程序的实例。                  |
|        程序是一个被动实体，因为它驻留在二级存储器中。        | 进程是一个主动实体，因为它是在执行过程中创建并加载到主内存中的。 |
|         程序存在于一个地方，并持续存在，直到被删除。         |       进程存在的时间有限，因为它在任务完成后会被终止。       |
|                        程序是静态的。                        |                        进程是动态的。                        |
|      程序没有任何资源要求，它只需要内存空间来存储指令。      | 进程对资源的要求很高，它在生命周期中需要CPU、内存地址、I/O等资源。 |
|                     程序没有任何控制块。                     |             进程有自己的控制块，称为进程控制块。             |



### 进程控制块

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