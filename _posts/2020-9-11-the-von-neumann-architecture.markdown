---
layout: post
title: The von Neumann architecture 
date: 2020-09-07 15:28:49 +0800
categories: Study
tags: Theory CPU I/O Memory COA
img: https://s1.ax1x.com/2020/09/11/wtHYbd.png
author: KCSIE
describe: 冯-诺依曼结构 (Computer Organization & Architecture-1/计算机组成与体系结构-1)
---

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/11/wtHYbd.png" alt="" />

## Overview
The von Neumann architecture—also known as the von 
Neumann model or Princeton architecture—is a computer 
architecture based on a 1945 description by Hungarian-American 
mathematician and physicist John von Neumann and others 
in the First Draft of a Report on the EDVAC. That document 
describes a design architecture for an electronic digital computer 
with these components:
+ A processing unit that contains an arithmetic logic unit and processor registers
    + Arithmetic Logical Unit(ALU)-Implementing arithmetic and logical operations
    + Program Status Word(PSW)-Presenting the status information of the current instruction execution result and storing the controlling information
+ A controller that contains an instruction register and program counter
    + Program Counter(PC)-Store the address of the instruction
	+ Control Unit(CU)
	  > - Instruction Register(IR)-Store the instruction
	  > - Instruction Decoder(ID)-Interpret the opcode of the instruction
	  > - Operation Controller(OC)-Produce operation control signals
+ Memory that stores data and instructions
  
    >Main memory -CPU has direct access to it
+ External mass storage
  
    >Secondary memory -The CPU can access it only after it is called into the main memory, e.g. hard disk
+ Input and output mechanisms
  
    >I/O modules-Move data between the computer and its external environment

Also, in addition to the processor and controller, the CPU has the following parts:
+ CPU Register
    + > Memory Adress Register(MAR)-It's the CPU register that either stores the memory address from which data will be fetched to the CPU, or the address to which data will be sent and stored. In other words, MAR holds the memory location of data that needs to be accessed. When reading from memory, data addressed by MAR is fed into the MDR (memory data register) and then used by the CPU. When writing to memory, the CPU writes data from MDR to the memory location whose address is stored in MAR. MAR, which is found inside the CPU, goes either to the RAM (random access memory) or cache
	+ > Memory Buffer/Data Register(MBR/MDR)- It's the register that stores the data being transferred to and from the immediate access storage. It contains the copy of designated memory locations specified by the memory address register. It acts as a buffer allowing the processor and memory units to act independently without being affected by minor differences in operation. A data item will be copied to the MBR ready for use at the next clock cycle, when it can be either used by the processor for reading or writing or stored in main memory after being written.
+ Cache
  
    >Cache is a component that stores data so that future requests for that data can be served faster; the data stored in a cache might be the result of an earlier computation or a copy of data stored elsewhere. A cache hit occurs when the requested data can be found in a cache, while a cache miss occurs when it cannot. Cache hits are served by reading data from the cache, which is faster than recomputing a result or reading from a slower data store; thus, the more requests that can be served from the cache, the faster the system performs

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/11/wt7Xjg.png" alt="" />

## 概述
冯-诺依曼体系结构--又称冯-诺依曼模型或普林斯顿体系结构，
是根据1945年美籍匈牙利数学家、物理学家约翰-冯-诺依曼等人在《EDVAC报告第一稿》
中的描述而提出的一种计算机体系结构，描述了一种电子计算机的设计体系结构，
其中包括这些组成部分：
+ 包含算术逻辑单元和程序状态寄存器的运算器
    + 算术逻辑单元(ALU)-实现算术运算和逻辑运算
	+ 程序状态寄存器(PSW)-体现当前指令执行结果的状态信息和存放控制信息
+ 包含指令寄存器和程序计数器的控制器
    + 程序计数器(PC)-存放指令地址
	+ 控制单元(CU)
	  > - 指令寄存器(IR)-存放指令
	  > - 指令译码器(ID)-分析解释指令的操作码
	  > - 操作控制器(OC)-产生操作控制信号
+ 存储数据和指令的存储器
  
    >主存储器(内存)-CPU可直接访问
+ 外部大容量存储
  
    >辅助存储器(外存)-调入主存后CPU才可访问,如硬盘
+ 输入和输出机制
  
    >输入/输出模块-使数据在计算机和其外部环境(外设)传输

同时，CPU除了运算器和控制器部分，还具有以下部分：
+ CPU寄存器
    + > 存储器地址寄存器(MAR)-存储需要被访问的数据的内存地址。当从内存读数据的时候，MAR处理的数据，就会被发送给MDR，然后被CPU使用。当将数据写入内存的时候，过程与之相反
    + > 存储器缓冲寄存器(MBR/MDR)-寄存了将要写入到电脑储贮(如：RAM)的数据或由电脑储贮读取后的数据。它就像缓冲器，数据在CPU和内存条所承载的内存介质之间交换时，要经过MDR，使之持有从内存复制的数据，以准备给处理器使用
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
+ Sending the required programs and data to the computer (Copy)
+ Must have the ability to remember programs, data, intermediate results and final calculations for a long period of time(Hard disk)
+ Be able to perform various arithmetic and logical operations and data processing such as data transfer (ALU)
+ Ability to control the direction of the program as required and to control the coordinated operation of the various components of the computer as directed
+ Be able to output the results of processing to the user as required

## 功能
+ 将需要的程序和数据传输送至计算机中（复制）
+ 必须具备长期记忆程序、数据、中间结果及最终运算结果的能力（硬盘）
+ 具有能够完成各种算术、逻辑运算和数据传送等数据加工处理的能力（ALU）
+ 可以根据需要控制程序的走向，并根据指令控制计算机的各部件协调操作
+ 能够按照要求将处理的结果输出给用户

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/13/wwXde0.jpg" alt="" />

## Execution
+ Instruction cycle  
   + The process of executing a program is actually a continuous process of fetching instructions, analyzing them, and executing them. Von Neumann type computers essentially work with a serial sequential processing mechanism, and must execute instruction sequences one by one even when the data in question is ready
   + The instruction cycle (also known as the fetch–decode–execute cycle, or simply the fetch-execute cycle) is the cycle that the central processing unit (CPU) follows from boot-up until the computer has shut down in order to process instructions. It is composed of three main stages: the fetch stage, the decode stage, and the execute stage
   + Summary of stages
	 - > Fetch Stage: The next instruction is fetched from the memory address that is currently stored in the program counter(PC) and stored into the instruction register(IR). At the end of the fetch operation, the PC points to the next instruction that will be read at the next cycle
     - > Decode Stage: During this stage, the encoded instruction presented in the instruction register(IR) interpreted by the decoder
     - > Execute Stage: The control unit of the CPU passes the decoded information as a sequence of control signals to the relevant function units of the CPU to perform the actions required by the instruction, such as reading values from registers, passing them to the ALU to perform mathematical or logic functions on them, and writing the result back to a register. If the ALU is involved, it sends a condition signal back to the CU. The result generated by the operation is stored in the main memory or sent to an output device. Based on the feedback from the ALU, the PC may be updated to a different address from which the next instruction will be fetched
     - > Repeat Cycle
+ Detail
    + > Enter sequences of instructions (programs) and original data into the computer's memory in advance which instruct the computer how to operate, with each instruction specifying the address from which the computer will fetch the number, what operation it will perform, and where it will send it to, etc
	+ > When the computer is executed, the first instruction is taken out of the memory, the requirements of the instruction are received through the controller's decoder, and then the data is taken out of the memory to perform the specified calculations and logical operations, etc., and then the result is sent to the memory at the address, and if it is necessary to store the data to a storage device such as a hard disk, it is also necessary to store that data in the memory to the hard disk. Next, the 2nd instruction is taken out, and the specified operation is completed under the command of the controller, and the sequence continues until a stop instruction is entered
	+ > There are two kinds of information flowing in a computer, one is data, i.e. various original data, intermediate results, programs, etc., and the other is information of control, which controls various parts of the machine to perform various operations specified by instructions

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/13/wwBTxI.png" alt="" />

## 执行
+ 指令周期
   + 程序的执行过程实际上是不断地取出指令、分析指令、执行指令的过程。冯·诺依曼型计算机从本质上讲是采用串行顺序处理的工作机制，即使有关数据已经准备好了，也必须逐条执行指令序列
   + 指令周期(又称读取-解码-执行周期，或简称读取-执行周期)是指中央处理单元(CPU)从开机到计算机关机为止，为了处理指令而遵循的周期。它由三个主要阶段组成：获取阶段、解码阶段和执行阶段
   + 阶段摘要
	 - > 读取阶段：从当前存储在程序计数器（PC）中的内存地址中获取下一条指令，并存储到指令寄存器（IR）中。在获取操作结束时，PC指向下一个周期将读取的下一条指令
     - > 解码阶段：在此阶段，解码器会解释指令寄存器（IR） 中显示的已编码指令
	 - > 执行阶段：CPU的控制单元将解码后的信息作为一连串的控制信号传递给CPU的相关功能单元，以执行指令所要求的操作，如从寄存器中读取数值，将数值传递给ALU对其执行数学或逻辑运算，并将结果写回寄存器。如果ALU参与其中，则会向CU发送条件信号。运算产生的结果存储在主存储器中，或送至输出设备。根据ALU的反馈，PC可能会更新到不同的地址，从这个地址获取下一条指令
	 - > 重复循环
+ 具体过程
    + > 预先把指挥计算机如何进行操作的指令序列（程序）和原始数据输入到计算机内存中，每条指令中明确规定了计算机从哪个地址取数，进行什么操作，然后送到什么地方去等步骤
	+ > 计算机在执行时，先从内存中取出第一条指令，通过控制器的译码器接收指令的要求，再从存储器中取出数据进行指定的运算和逻辑操作等，然后再按地址把结果送到内存中，如果需要向硬盘等存储设备存储数据，还需要将内存中的该数据存储到硬盘中。接下来取出第2条指令，在控制器的指挥下完成规定操作，依次进行下去，直到遇到停止指令
	+ > 计算机中有两种信息在流动，一种是数据，即各种原始数据、中间结果和程序等，另一种信息是控制信息，它控制机器的各种部件执行指令规定的各种操作
	

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/13/wwjkmq.jpg" alt="" />	
	
<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/14/wsPqHS.png" alt="" />		
	
	
	