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

