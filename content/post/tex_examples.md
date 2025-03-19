---
date: '2025-03-18T20:51:32+08:00'
draft: false
title: 'Tex公式书写示例'
categories:
  - math
tags:
  - tex
keywords:
  - tex
  - mathjax
description: 'Tex公式示例'
mathjax: true
---

## 空格

$a\ b$ 表示空格，1/3m宽度

$a\;b$ 表示中等空格，2/7m宽度

## 极限/微积分

$\exists\ \xi \in S$

$\forall\ x\in S$

导数 (Derivative), 连续(Continuity), 极限(Limit, Left-hand Limit, Right-hand Limit)：

$$
f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h} \\
\lim_{x \to a} f(x) = f(a) \\
\lim_{x \to a^-} f(x) \\
\lim_{x \to a^+} f(x) \\
\lim_{x \to \infty} f(x) \\
\lim_{x \to a} f(x) = 0
$$

积分(Integral):

$$
\int f(x) \, dx \\
\int_{a}^{b} f(x) \, dx
$$

微分(Differential), 泰勒级数:

$$
dy = f'(a) \, dx \\
f(x) = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \frac{f'''(a)}{3!}(x-a)^3 + \cdots
$$

偏导（Partial Derivative）

$$
\frac{\partial f}{\partial x} \\
\frac{\partial f}{\partial y}
$$

多重积分 (Multiple Integrals)

$$
\iint_D f(x, y) \, dA \\
\iiint_V f(x, y, z) \, dV
$$


## 矩阵/向量

矩阵定义:

$$
A = \begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33}
\end{pmatrix}
$$

矩阵转置:

$$
A^T = \begin{pmatrix}
a_{11} & a_{21} & a_{31} \\
a_{12} & a_{22} & a_{32} \\
a_{13} & a_{23} & a_{33}
\end{pmatrix}
$$

矩阵乘法:

$$
C = AB \\
c_{ij} = \sum_{k=1}^{n} a_{ik} b_{kj}
$$

逆矩阵:
$$
AA^{-1} = A^{-1}A = I
$$

向量定义:

$$
\mathbf{v} = \begin{pmatrix}
v_1 \\
v_2 \\
v_3
\end{pmatrix}
$$

向量加法:

$$
\mathbf{u} + \mathbf{v} = \begin{pmatrix}
u_1 \\
u_2 \\
u_3
\end{pmatrix} + \begin{pmatrix}
v_1 \\
v_2 \\
v_3
\end{pmatrix} = \begin{pmatrix}
u_1 + v_1 \\
u_2 + v_2 \\
u_3 + v_3
\end{pmatrix}
$$

向量点积:

$$
\mathbf{u} \cdot \mathbf{v} = u_1 v_1 + u_2 v_2 + u_3 v_3
$$

向量叉积:

$$
\mathbf{u} \times \mathbf{v} = \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
u_1 & u_2 & u_3 \\
v_1 & v_2 & v_3
\end{vmatrix} = \begin{pmatrix}
u_2 v_3 - u_3 v_2 \\
u_3 v_1 - u_1 v_3 \\
u_1 v_2 - u_2 v_1
\end{pmatrix}
$$

向量长度:

$$
\|\mathbf{v}\| = \sqrt{v_1^2 + v_2^2 + v_3^2}
$$

## 概率与统计

单个随机变量 $X$ 的期望、方差，标准差

$$
\mathbb{E}[X] = \sum_{i} x_i P(X = x_i) \\
\text{Var}(X) = \mathbb{E}[(X - \mathbb{E}[X])^2] \\
\sigma_X = \sqrt{\text{Var}(X)}
$$

两个随机变量$X$ 和 $Y$ 的协方差，相关系数

$$
\text{Cov}(X, Y) = \mathbb{E}[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])] \\
\rho_{X,Y} = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}
$$

常见分布：二项分布，正态分布

$$
P(X = k) = \binom{n}{k} p^k (1 - p)^{n - k} \quad \text{for } k = 0, 1, 2, \ldots, n
f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}
$$

大数定理: 如果 $X_1, X_2, \ldots, X_n$ 是独立同分布的随机变量，其期望值为 $\mu$，则：

$$
\frac{1}{n} \sum_{i=1}^n X_i \xrightarrow{n \to \infty} \mu
$$

中心极限定理: 如果 $X_1, X_2, \ldots, X_n$ 是独立同分布的随机变量，其期望值为 $\mu$，标准差为 $\sigma$，则：

$$
\frac{\sum_{i=1}^n X_i - n\mu}{\sqrt{n}\sigma} \xrightarrow{d} \mathcal{N}(0, 1) \quad \text{as } n \to \infty
$$

贝叶斯定理:

$$
P(A|B) = \frac{P(B|A)P(A)}{P(B)}
$$


