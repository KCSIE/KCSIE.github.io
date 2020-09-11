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
    >Arithmetic Logical Unit(ALU)-Implementing arithmetic and logical operations
	>Program Status Word(PSW)-Presenting the status information of the current instruction execution result and storing the controlling information
+ A controller that contains an instruction register and program counter
    >Program Counter(PC)-Store the address of the instruction
	>Control Unit(CU)
	>>Instruction Register(IR)-Store the instruction
	>>Instruction Decoder(ID)-Interpret the opcode of the instruction
	>>Operation Controller(OC)-Produce operation control signals
+ Memory that stores data and instructions
    >Main memory -CPU has direct access to it
+ External mass storage
    >Secondary memory -The CPU can access it only after it is called into the main memory, e.g. hard disk
+ Input and output mechanisms

## 概述
冯-诺依曼体系结构--又称冯-诺依曼模型或普林斯顿体系结构，
是根据1945年美籍匈牙利数学家、物理学家约翰-冯-诺依曼等人在《EDVAC报告第一稿》
中的描述而提出的一种计算机体系结构，描述了一种电子计算机的设计体系结构，
其中包括这些组成部分：
+ 一个处理单元，包含一个算术逻辑单元和程序状态寄存器
    >算术逻辑单元(ALU)-实现算术运算和逻辑运算
	>程序状态寄存器(PSW)-体现当前指令执行结果的状态信息和存放控制信息
+ 包含指令寄存器和程序计数器的控制器
    >程序计数器(PC)-存放指令地址
	>控制单元(CU)
	>>指令寄存器(IR)-存放指令
	>>指令译码器(ID)-分析解释指令的操作码
	>>操作控制器(OC)-产生操作控制信号
+ 存储数据和指令的存储器
    >主存储器(内存)-CPU可直接访问
+ 外部大容量存储
    >辅助存储器(外存)-调入主存后CPU才可访问,如硬盘
+ 输入和输出机制

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/09/11/wt7Xjg.png" alt="" />
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

## 



