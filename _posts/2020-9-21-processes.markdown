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

```
| Program | Process |
|  :---:  |  :---:  |
| When we execute a program that was just compiled, the OS will generate a process to execute the program. Execution of the program starts via GUI mouse clicks, command line entry of its name, etc. A program is a passive entity as it resides in the secondary memory, such as the contents of a file stored on disk. One program can have several processes. | The term process (Job) refers to program code that has been loaded into a computer’s memory so that it can be executed by the central processing unit (CPU). A process can be described as an instance of a program running on a computer or as an entity that can be assigned to and executed on a processor. A program becomes a process when loaded into memory and thus is an active entity. |
| Program contains a set of instructions designed to complete a specific task.  | Process is an instance of an executing program. |
| Program is a passive entity as it resides in the secondary memory.  | Process is a active entity as it is created during execution and loaded into the main memory. |
| Program exists at a single place and continues to exist until it is deleted.  | Process exists for a limited span of time as it gets terminated after the completion of task. |
| Program is a static entity.  | Process is a dynamic entity. |
| Program does not have any resource requirement, it only requires memory space for storing the instructions.  | Process has a high resource requirement, it needs resources like CPU, memory address, I/O during its lifetime. |
| Program does not have any control block.  | Process has its own control block called Process Control Block. |
```