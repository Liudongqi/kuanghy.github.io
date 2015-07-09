---
layout: post
title: 进程与线程概念理解浅析
category: 计算机科学
tags: 进程 线程
---

## 进程
**进程**（Process）是计算机中的程序关于某数据集合上的一次运行活动，`是系统进行资源分配和调度的基本单位`，是操作系统结构的基础。在早期面向进程设计的计算机结构中，进程是程序的基本执行实体；在当代面向线程设计的计算机结构中，进程是线程的容器。程序是指令、数据及其组织形式的描述，进程是程序的实体。

进程，是并发执行的程序在执行过程中分配和管理资源的基本单位，是一个动态概念，`竟争计算机系统资源的基本单位`。每一个进程都有一个自己的地址空间，即进程空间或（虚空间）。进程空间的大小只与处理机的位数有关，一个 16 位长处理机的进程空间大小为 216 ，而 32 位处理机的进程空间大小为 232 。进程至少有 5 种基本状态，它们是：初始态，执行态，等待状态，就绪状态，终止状态。

![process state](http://ww2.sinaimg.cn/mw690/c3c88275jw1etwmdm9kwuj20be03lq2z.jpg)

进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动,进程是系统进行资源分配和调度的一个独立单位。

<br/>
## 线程
线程，有时被称为轻量级进程(Lightweight Process，LWP），`是程序执行流的最小单元`。一个标准的线程由线程ID，当前指令指针(PC），寄存器集合和堆栈组成。另外，线程是进程中的一个实体，是被系统独立调度和分派的基本单位，线程自己不拥有系统资源，只拥有一点儿在运行中必不可少的资源，但它可与同属一个进程的其它线程共享进程所拥有的全部资源。一个线程可以创建和撤消另一个线程，同一进程中的多个线程之间可以并发执行。由于线程之间的相互制约，致使线程在运行中呈现出间断性。线程也有就绪、阻塞和运行三种基本状态。就绪状态是指线程具备运行的所有条件，逻辑上可以运行，在等待处理机；运行状态是指线程占有处理机正在运行；阻塞状态是指线程在等待一个事件（如某个信号量），逻辑上不可执行。每一个程序都至少有一个线程，若程序只有一个线程，那就是程序本身。

![thread state](http://ww1.sinaimg.cn/mw690/c3c88275jw1etwm7owjzlj20hs0c3jsc.jpg)

线程，在网络或多用户环境下，一个服务器通常需要接收大量且不确定数量用户的并发请求，为每一个请求都创建一个进程显然是行不通的，——无论是从系统资源开销方面或是响应用户请求的效率方面来看。因此，操作系统中线程的概念便被引进了。线程，是进程的一部分，一个没有线程的进程可以被看作是单线程的。线程有时又被称为轻权进程或轻量级进程，也是 CPU 调度的一个基本单位。

线程是进程的一个实体,是CPU调度和分派的基本单位,它是比进程更小的能独立运行的基本单位.线程自己基本上不拥有系统资源,只拥有一点在运行中必不可少的资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源.

<br/>
## 线程与进程的区别和联系
通常在一个进程中可以包含若干个线程，它们可以利用进程所拥有的资源，在引入线程的操作系统中，通常都是`把进程作为分配资源的基本单位`，而`把线程作为独立运行和独立调度的基本单位`，由于线程比进程更小，基本上不拥有系统资源，故对它的调度所付出的开销就会小得多，能更高效的提高系统内多个程序间并发执行的程度。

进程的执行过程是线状的，尽管中间会发生中断或暂停，但该进程所拥有的资源只为该线状执行过程服务。一旦发生进程上下文切换，这些资源都是要被保护起来的。这是进程宏观上的执行过程。而进程又可有单线程进程与多线程进程两种。我们知道，进程有 一个进程控制块 PCB ，相关程序段 和 该程序段对其进行操作的数据结构集 这三部分，单线程进程的执行过程在宏观上是线性的，微观上也只有单一的执行过程；而多线程进程在宏观上的执行过程同样为线性的，但微观上却可以有多个执行操作（线程），如不同代码片段以及相关的数据结构集。**线程的改变只代表了 CPU 执行过程的改变，而没有发生进程所拥有的资源变化**。出了 CPU 之外，**计算机内的软硬件资源的分配与线程无关，线程只能共享它所属进程的资源**。与进程控制表和 PCB 相似，每个线程也有自己的线程控制表 TCB ，而这个 TCB 中所保存的线程状态信息则要比 PCB 表少得多，这些信息主要是相关指针用堆栈（系统栈和用户栈），寄存器中的状态数据。**进程拥有一个完整的虚拟地址空间，不依赖于线程而独立存在；反之，线程是进程的一部分，没有自己的地址空间，与进程内的其他线程一起共享分配给该进程的所有资源**。

单个CPU一次只能运行一个任务。这里不能简单的理解为一次只能运行一个进程，这里的任务是指独立运行和独立调度的基本单位。在引入线程的操作系统中，这里的任务应该是指线程，如果是单线程的也可以认为就是进程。

**线程与进程的区别归纳：**
> 1. 地址空间和其它资源：进程间相互独立，同一进程的各线程间共享。某进程内的线程在其它进程不可见。

> 2. 通信：进程间通信IPC，线程间可以直接读写进程数据段（如全局变量）来进行通信——需要进程同步和互斥手段的辅助，以保证数据的一致性。

> 3. 调度和切换：线程上下文切换比进程上下文切换要快得多。

> 4. 在多线程OS中，进程不是一个可执行的实体。即在支持线程的操作系统中，线程是程序独立运行和独立调度的基本单位。

<br/>
## 参考资料
http://www.cnblogs.com/way_testlife/archive/2011/04/16/2018312.html
http://blog.csdn.net/yaosiming2011/article/details/44280797
http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html
百度百科：[进程](http://baike.baidu.com/view/19746.htm)，[线程](http://baike.baidu.com/view/1053.htm)