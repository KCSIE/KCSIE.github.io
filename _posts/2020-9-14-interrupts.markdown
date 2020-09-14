---
layout: post
title: Interrupts
date: 2020-09-09 20:52:49 +0800
categories: Study
tags: Theory CPU I/O Memory ComputerScience
img: https://s1.ax1x.com/2020/09/14/wrqgwq.png
author: KCSIE
describe: 中断
---

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/14/wrqgwq.png" alt="" />

## Introduction
The instruction cycle is formed when the CPU executes instructions as follows:
+ > Before the program is executed, the beginning address of the program is sent to the program counter. This address is determined when the program is loaded into memory, so the first thing stored in the program counter is the address of the first instruction in the program. This address is sent to the system bus to complete the fetch operation
+ > The fetched instructions are temporarily stored in the instruction register
+ > The instruction decoder gets the instruction from the instruction register and analyzes the operation code and the address code of the instruction. Then the CPU finds the operation to be performed by the instruction according to the analyzed opcode and finds the required data according to the address code to complete the instruction execution
+ > The program counter is added by 1 or according to the transfer instruction to get the address of the next instruction, and then the next instruction is executed until the whole program is finished

During the execution process, the central processor and memory may receive asynchronous signals from the peripheral hardware or synchronous signals from the software, so the CPU suspends the program being executed while performing the corresponding hardware/software processing, and then resumes the previous program when this execution is complete.In short, the processor receives a signal from hardware or software that an event has occurred and should be noticed, which is called an interrupt

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/14/wrqhfU.png" alt="" />

## 引入
在CPU如下执行指令时，形成了指令周期：
+ > 在程序执行之前，会将程序的起始地址送入程序计数器中，该地址在程序加载到内存时确定，所以程序计数器中首先存的是程序第一条指令的地址。将该地址送往地址总线，完成取指操作
+ > 取来的指令暂存到指令寄存器中
+ > 指令译码器从指令寄存器中得到指令，分析指令的操作码和地址码。然后 CPU 根据分析的操作码知道该条指令要进行的操作，根据地址码找到需要的数据，完成指令的执行
+ > 程序计数器加1或根据转移指令得到下一条指令的地址，接下来再进行下一条指令的执行，直到整个程序执行完成

在运行过程中，中央处理器和内存可能会接收到来自外围硬件的异步信号或来自软件的同步信号，因此CPU会暂停正在执行的程序，而进行相应的硬件/软件处理，当这段程序执行完毕后再继续执行之前的程序。简单来说，处理器接收到来自硬件或软件的信号，提示发生了某个事件，应该被注意，这种情况就称为中断

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/14/wsSC26.png" alt="" />

## Overview
Interrupting is an important technique used to improve the efficiency and functionality of a computer. Hardware interrupts were originally introduced for the sake of performance only. If there were no interrupts in a computer system, a processor communicating with an external device would have to do a busy waiting after issuing a command to the device, repeatedly polling the device to see if it had completed its action and returning the result. This results in a lot of wasted processor cycles. With the introduction of interrupts, the processor can return immediately after the device request to process another task, and when the device completes its action, it sends an interrupt to the processor, which can then go back and get the result. In this way, during the processing cycle of the device, the processor can perform some other meaningful work at a small time cost caused by the switch. It was later used in a number of ways for external and internal CPU emergencies, machine failures, time control, etc., and gave rise to the concept of entering interrupt processing (soft interrupts) via software

In terms of hardware implementation, the interrupt can be a stand-alone system containing control lines or it can be integrated into a memory subsystem. For the former, on IBM personal machines, a programmable interrupt controller (PIC) is widely used for interrupt response and processing.The PIC is connected between a number of interrupt request devices and the interrupt pins of the processor, thus enabling multiplexing of the processor's interrupt request lines (mostly one or two pins). As another form of interrupt implementation, a memory subsystem implementation, the interrupt port can be mapped to the address space of the memory so that access to a particular memory address is actually an interrupt request

In simple terms, interruptions have the following main benefits:
+ Most I/O devices are slower than the processor，so interrupt can improve CPU’s utilization
+ Count
+ Avoid some program to monopolize CPU 


## 总览
中断是用以提高计算机工作效率、增强计算机功能的一项重要技术。最初引入硬件中断，只是出于性能上的考量。如果计算机系统没有中断，则处理器与外部设备通信时，它必须在向该设备发出指令后进行忙等待（Busy waiting），反复轮询该设备是否完成了动作并返回结果。这就造成了大量处理器周期被浪费。引入中断以后，当处理器发出设备请求后就可以立即返回以处理其他任务，而当设备完成动作后，发送中断信号给处理器，后者就可以再回过头获取处理结果。这样，在设备进行处理的周期内，处理器可以执行其他一些有意义的工作，而只付出一些很小的切换所引发的时间代价。后来被用于CPU外部与内部紧急事件的处理、机器故障的处理、时间控制等多个方面，并产生通过软件方式进入中断处理（软中断）的概念。

在硬件实现上，中断可以是一个包含控制线路的独立系统，也可以被集成进存储器子系统中。对于前者，在IBM个人机上，广泛使用可编程中断控制器（Programmable Interrupt Controller，PIC）来负责中断响应和处理。PIC被连接在若干中断请求设备和处理器的中断引脚之间，从而实现对处理器中断请求线路（多为一针或两针）的复用。作为另一种中断实现的形式，即存储器子系统实现方式，可以将中断端口映射到存储器的地址空间，这样对特定存储器地址的访问实际上是中断请求。

简单来说，中断的有如下主要好处：
+ 提高CPU利用率
+ 计数时钟中断
+ 避免CPU被独占










