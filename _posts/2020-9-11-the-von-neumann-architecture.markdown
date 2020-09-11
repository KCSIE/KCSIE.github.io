---
layout: post
title: The von Neumann architecture
date: 2020-09-07 15:28:49 +0800
categories: Study
tags: Theory CPU ComputerScience
img: https://s1.ax1x.com/2020/09/11/wtHYbd.png
author: KCSIE
describe: 冯-诺依曼结构
---

## Overview
The von Neumann architecture—also known as the von 
Neumann model or Princeton architecture—is a computer 
architecture based on a 1945 description by Hungarian-American 
mathematician and physicist John von Neumann and others 
in the First Draft of a Report on the EDVAC. That document 
describes a design architecture for an electronic digital computer 
with these components:
+ A processing unit that contains an arithmetic logic unit and processor registers
    > + Arithmetic Logical Unit(ALU)-Implementing arithmetic and logical operations
	> + Program Status Word(PSW)-Presenting the status information of the current instruction execution result and storing the controlling information
+ A controller that contains an instruction register and program counter
    > + Program Counter(PC)-Store the address of the instruction
	> + Control Unit(CU)
	>> - Instruction Register(IR)-Store the instruction
	>> - Instruction Decoder(ID)-Interpret the opcode of the instruction
	>> - Operation Controller(OC)-Produce operation control signals
+ Memory that stores data and instructions
    >Main memory -CPU has direct access to it
+ External mass storage
    >Secondary memory -The CPU can access it only after it is called into the main memory, e.g. hard disk
+ Input and output mechanisms
    >I/O modules-Move data between the computer and its external environment

Also, in addition to the processor and controller, the CPU has the following parts:
+ CPU Register
    > + Memory Adress Register(MAR)-It's the CPU register that either stores the memory address from which data will be fetched to the CPU, or the address to which data will be sent and stored. In other words, MAR holds the memory location of data that needs to be accessed. When reading from memory, data addressed by MAR is fed into the MDR (memory data register) and then used by the CPU. When writing to memory, the CPU writes data from MDR to the memory location whose address is stored in MAR. MAR, which is found inside the CPU, goes either to the RAM (random access memory) or cache
	> + Memory Buffer/Data Register(MBR/MDR)- It's the register that stores the data being transferred to and from the immediate access storage. It contains the copy of designated memory locations specified by the memory address register. It acts as a buffer allowing the processor and memory units to act independently without being affected by minor differences in operation. A data item will be copied to the MBR ready for use at the next clock cycle, when it can be either used by the processor for reading or writing or stored in main memory after being written.
+ Cache
    >Cache is a component that stores data so that future requests for that data can be served faster; the data stored in a cache might be the result of an earlier computation or a copy of data stored elsewhere. A cache hit occurs when the requested data can be found in a cache, while a cache miss occurs when it cannot. Cache hits are served by reading data from the cache, which is faster than recomputing a result or reading from a slower data store; thus, the more requests that can be served from the cache, the faster the system performs

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/11/wt7Xjg.png" alt="" />

## 概述
冯-诺依曼体系结构--又称冯-诺依曼模型或普林斯顿体系结构，
是根据1945年美籍匈牙利数学家、物理学家约翰-冯-诺依曼等人在《EDVAC报告第一稿》
中的描述而提出的一种计算机体系结构，描述了一种电子计算机的设计体系结构，
其中包括这些组成部分：
+ 包含算术逻辑单元和程序状态寄存器的运算器
    > + 算术逻辑单元(ALU)-实现算术运算和逻辑运算
	> + 程序状态寄存器(PSW)-体现当前指令执行结果的状态信息和存放控制信息
+ 包含指令寄存器和程序计数器的控制器
    > + 程序计数器(PC)-存放指令地址
	> + 控制单元(CU)
	>> - 指令寄存器(IR)-存放指令
	>> - 指令译码器(ID)-分析解释指令的操作码
	>> - 操作控制器(OC)-产生操作控制信号
+ 存储数据和指令的存储器
    >主存储器(内存)-CPU可直接访问
+ 外部大容量存储
    >辅助存储器(外存)-调入主存后CPU才可访问,如硬盘
+ 输入和输出机制
    >输入/输出模块-使数据在计算机和其外部环境(外设)传输

同时，CPU除了运算器和控制器部分，还具有以下部分：
+ CPU寄存器
    > + 存储器地址寄存器(MAR)-存储需要被访问的数据的内存地址。当从内存读数据的时候，MAR处理的数据，就会被发送给MDR，然后被CPU使用。当将数据写入内存的时候，过程与之相反
	> + 存储器缓冲寄存器(MBR/MDR)-寄存了将要写入到电脑储贮(如：RAM)的数据或由电脑储贮读取后的数据。它就像缓冲器，数据在CPU和内存条所承载的内存介质之间交换时，要经过MDR，使之持有从内存复制的数据，以准备给处理器使用
+ 高速缓冲存储器
    >也叫缓存(Cache)，其原始意义是指存取速度比一般随机存取记忆体(RAM)来得快的一种RAM，一般而言它不像系统主记忆体那样使用DRAM技术，而使用昂贵但较快速的SRAM技术，也有快取记忆体的名称。提供“缓存”的目的是为了让数据访问的速度适应CPU的处理速度，当CPU处理数据时，它会先到Cache中去寻找，如果数据因之前的操作已经读取而被暂存其中，就不需要再从随机存取存储器中读取数据

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/11/wNzDcn.png" alt="" />

## Trait
+ All data and instructions processed by the cpu are expressed in binary
+ Instructions and data are indiscriminately mixed and stored in the same memory （All can be found by address）
+ Sequentially execute each instruction of the program （Instructions are pre-entered 
into the computer's main memory in the form of a code, 
and then the first instruction of the program is 
executed at its first address in memory, and the other 
instructions are executed in the sequence set forth in 
the program until the end of the program）
+ The execution order can be changed under certain conditions 
according to the results of calculations or the preset 
conditions

## 特点
+ CPU处理的数据和指令一律用二进制表示
+ 指令和数据不加区别混合存储在同一个存储器
+ 顺序执行程序的每一条指令
+ 在特定条件下可根据运算结果或设定条件改变执行顺序

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/11/wUA9kq.png" alt="" />

## Function
+

## 功能
 



