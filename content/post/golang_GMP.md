---
date: '2025-05-06T10:56:18+08:00'
draft: false
title: 'Golang GMP原理解析'
categories:
  - tech
keywords:
  - Golang
  - GMP
tags:
  - Golang
  - GMP
---

# 基础知识

## 线程 vs. 协程

- 线程Thread是操作系统内核视角下的**最小调度单元**，其创建、销毁、切换、调度都需要由内核参与；
- 协程可以理解为用户态线程，是用户程序对对线程概念的二次封装，和线程为多对一关系，在逻辑意义上属于更细粒度的调度单元，其调度过程由**用户态闭环完成**，无需内核介入

> 协程可以作为实现用户态线程的基础，但是不是等于是用户态线程。“User-level threads are different from coroutines. Coroutines voluntarily yield to each other; user-level threads can preempt or be preempted.” --MIT 6.828 Operating System

## goroutine与GMP架构

goroutine 是其对协程的本土化实现，并且在原生协程的基础上做了很大的优化改进，其本身依附于GMP（goroutine-machine-processor）体系而生。GMP架构使得goroutine相比原生协程具有如下优势：

- g 与 p、m 之间可以动态结合，整个调度过程有着很高的灵活性
- g 栈空间大小可以动态扩缩，既能做到使用方便，也尽可能地节约了资源

GMP = goroutine + machine + processor, 其三个核心组件

1. g
    - g即goroutine, 是golang中对于协程的抽象
    - g 有自己的运行栈、生命周期状态、以及执行的任务函数（用户通过`go func`指定）
    - g 需要绑定在 m 上执行，在 g 视角中，可以将 m 理解为它的 cpu
2. m
    - 
3. p

## GMP设计精髓

GMP内存管理：

GMP并发工具

IO多路复用



# 调度原理
