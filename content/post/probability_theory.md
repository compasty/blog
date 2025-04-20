---
date: '2025-04-01T20:44:58+08:00'
draft: false
title: '概率论概要'
categories:
  - math
keywords:
  - probability
tags:
  - probability
mathjax: true
---

# 随机变量random variable

随机random vs. 规律deterministic

不同的思维决定了不同的策略，例如红球R和绿球G以RRGRRGRRG的方式出现，很多时候我们会认为规律的结构。但是如果以随机的角度来看，这个事情也是有可能发生的，概率为$P(\underline{RRGRRGRRG})=\left[\left(\frac{2}{3}\right)^2\left(\frac{1}{3}\right)\right]^3=\underline{0.325\%}$。


Q1: 丢硬币正面的概率是$\frac{2}{3}$, 如何预测每次的结果使得猜中的概率最大？
A1: 永远猜正面
证明: 设硬币的概率分布$X_{i}$, 预测策略的概率分布$Y_{i}$分别为: 

$$
\underline{X_i}=\left\{
\begin{array}
{ll}\underline{R}, & \mathrm{with~prob.}\underline{p}, \\
\underline{G}, & \mathrm{with~prob.}\underline{1-p}.
\end{array}\right. \\
\underline{Y_i}=\left\{
\begin{array}
{ll}\underline{R}, & \mathrm{with~prob.}\underline{q}, \\
\underline{G}, & \mathrm{with~prob.}\underline{1-q}.
\end{array}\right.
$$

则有:

$$
\begin{array}
{rcl}P(\underline{X_{i}=Y_{i}}) & = & P(\underline{(X_{i},Y_{i})}\in\{\underline{(G,G),(R,R)}\}) \\
& = & pq+(1-p)(1-q) \\
& = & 1-p + (2p - 1)q
\end{array}
$$

因此有$P(\underline{X_{i}=Y_{i}})$最大值为：

$$
\underline{q}=\left\{
\begin{array}
{ll}\underline{1}, & \mathrm{if}p>0.5, \\
\underline{0}, & \mathrm{if}\underline{p<0.5}.
\end{array}\right.
$$


# 参考

1. [概率论-新竹清华大学-郑少为](https://www.bilibili.com/video/BV1e4411X7x6)


