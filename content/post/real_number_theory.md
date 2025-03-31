---
date: '2025-03-18T20:51:32+08:00'
draft: false
title: '实数理论基础'
categories:
  - math
keywords:
  - real analysis
tags:
  - real analysis
description: '实数基础定理'
mathjax: true
---

## 基础

### 七大定理

1. Dedekind分割定理
2. 确界定理
3. Cauchy定理
4. 闭区间套定理
5. 单调有界定理
6. Heine-Borel定理
7. Bolzano-Weierstrass定理

### 最大数与最小数

定义1：设$S$使一个数集（R的子集），如果$\exists \xi \in S$，使得$\forall x\in S,x\le \xi$,则称$\xi$是数集$S$的最大数，记为:$\xi =max S$

如果$S$是非空有限集(只包含有限个数)时,$min S,max S$显然存在.当$S$是无限集时,最大数和最小数则不一定存在。

例如：集合$A=\{x\mid 0\le x<1\}$没有最大数.

证明：假设集合存在最大数$\beta$, 则有$\beta^{'}=\frac{1+\beta}{2}\in[0,1)$ 比$\beta$大，故矛盾

### 上下确界

确界的定义：设$S$是一个非空数集,如果$\exists M \in R: \forall x\in S,x\le M$,则称$M$为$S$的一个上界.类似地可以定义下界.当集合$S$的上下界均存在时,称$S$为有界集.

设非空数集$S$全体上界组成的集合为$U$,$U$没有最大数,但一定有最小数,这个最小数称为$S$的上确界,记为$\beta =sup\ S$.类似地,下确界为全体下界的最大数,记为$\alpha = inf\ S$.

### 有理数

1. 有理数的稠密性
稠密性的概念：在实数轴上，任意两个不相等的有理数之间都存在另一个有理数。换句话说，对于任意两个有理数$a$和$b$（其中$a < b$），总存在一个有理数$c$，使得 $a < c < b$。这意味着有理数在实数轴上是密集分布的，无论两个有理数之间的距离有多小，总能够找到另一个有理数
证明：取$c=\frac{a+b}{2}$即可

2. 有理数不具有连续性，比如$\sqrt{2}$就不是有理数

## Dedekind分割定理

## 确界定理
