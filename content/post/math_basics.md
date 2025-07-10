---
date: '2025-07-10T13:33:25+08:00'
draft: false
title: '数学基础定义&定理整理'
categories:
  - math
keywords:
  - Trigonometric functions
  - Inequality
tags:
  - Trigonometric functions
  - Inequality
mathjax: true
---

## 1. 三角函数

基础定义:
- $\tan \theta = \frac{\sin \theta}{\cos \theta}$
- $\csc \theta = \frac{1}{\sin \theta}, \quad \sec \theta = \frac{1}{\cos \theta}, \quad \cot \theta = \frac{1}{\tan \theta} = \frac{\cos \theta}{\sin \theta}$

基本恒等式:

1. **毕达哥拉斯恒等式**: $\sin^2 \theta + \cos^2 \theta = 1$

2. 和差公式: 

\\[
\begin{aligned}
\sin(\alpha \pm \beta) &= \sin \alpha \cos \beta \pm \cos \alpha \sin \beta \\\\
\cos(\alpha \pm \beta) &= \cos \alpha \cos \beta \mp \sin \alpha \sin \beta \\\\
\tan(\alpha \pm \beta) &= \frac{\tan \alpha \pm \tan \beta}{1 \mp \tan \alpha \tan \beta}
\end{aligned}
\\]

3. 由和差公式推导出来的倍角和半角公式公式:

\\[
\begin{aligned}
\sin 2\theta &= 2 \sin \theta \cos \theta \\\\
\cos 2\theta &= \cos^2 \theta - \sin^2 \theta = 2 \cos^2 \theta - 1 = 1 - 2 \sin^2 \theta \\\\
\tan 2\theta &= \frac{2 \tan \theta}{1 - \tan^2 \theta} \\\\
\sin^2 \frac{\theta}{2} &= \frac{1 - \cos \theta}{2} \\\\
\cos^2 \frac{\theta}{2} &= \frac{1 + \cos \theta}{2} \\\\
\tan \frac{\theta}{2} &= \pm \sqrt{\frac{1 - \cos \theta}{1 + \cos \theta}} = \frac{\sin \theta}{1 + \cos \theta} = \frac{1 - \cos \theta}{\sin \theta} \\\\
\sin \alpha \sin \beta &= \frac{1}{2} [\cos(\alpha - \beta) - \cos(\alpha + \beta)] \\\\
\cos \alpha \cos \beta &= \frac{1}{2} [\cos(\alpha - \beta) + \cos(\alpha + \beta)] \\\\
\sin \alpha \cos \beta &= \frac{1}{2} [\sin(\alpha + \beta) + \sin(\alpha - \beta)] \\\\
\end{aligned}
\\]

## 2. 不等式

### 2.1 三角不等式

对于任意实数 $a, b$，有：

\\[
|a + b| \leq |a| + |b|
\\]

几何意义：两点之间的距离不超过经过第三点的路径长度。

### 2.2 柯西-施瓦茨不等式（Cauchy–Schwarz Inequality）

对于实数或复数序列 $\{a_i\}, \{b_i\}$，有：

\\[
\left|\sum_{i=1}^n a_i b_i\right| \leq \sqrt{\sum_{i=1}^n a_i^2} \cdot \sqrt{\sum_{i=1}^n b_i^2}
\\]

等号成立当且仅当两个向量线性相关。

函数形式：对于可积函数 $f, g$，有：

\\[
\left|\int f(x) g(x) dx \right| \leq \sqrt{\int |f(x)|^2 dx} \cdot \sqrt{\int |g(x)|^2 dx}
\\]

---

### 2.3 均值不等式（AM-GM不等式）

对于非负实数 $a_1, a_2, \dots, a_n \geq 0$，有：

\\[
\frac{a_1 + a_2 + \cdots + a_n}{n} \geq \sqrt[n]{a_1 a_2 \cdots a_n}
\\]

等号成立当且仅当 $a_1 = a_2 = \cdots = a_n$。

### 2.4 赫尔德不等式（Hölder Inequality）

对于 $p, q > 1$，且 $\frac{1}{p} + \frac{1}{q} = 1$，有：

\\[
\sum_{i=1}^n |a_i b_i| \leq \left(\sum_{i=1}^n |a_i|^p\right)^{\frac{1}{p}} \cdot \left(\sum_{i=1}^n |b_i|^q\right)^{\frac{1}{q}}
\\]

### 2.5 明可夫斯基不等式（Minkowski Inequality）

对于 \\(p \geq 1\\)，有：

\\[
\left(\sum_{i=1}^n |a_i + b_i|^p\right)^{\frac{1}{p}} \leq \left(\sum_{i=1}^n |a_i|^p\right)^{\frac{1}{p}} + \left(\sum_{i=1}^n |b_i|^p\right)^{\frac{1}{p}}
\\]

### 2.6 伯努利不等式

对于实数 \\(x \geq -1\\) 和整数 \\(r \geq 0\\)，有：

\\[
(1 + x)^r \geq 1 + r x
\\]

等号成立当且仅当 \\(x = 0\\) 或 \\(r=0,1\\)。


### 2.7 切比雪夫不等式（Chebyshev's Inequality）

对于两个同向排序的数列 \\(a_1 \geq a_2 \geq \cdots \geq a_n\\) 和 \\(b_1 \geq b_2 \geq \cdots \geq b_n\\)，有：

\\[
\frac{1}{n} \sum_{i=1}^n a_i b_i \geq \left(\frac{1}{n} \sum_{i=1}^n a_i\right) \left(\frac{1}{n} \sum_{i=1}^n b_i\right)
\\]

### 2.8 詹森不等式（Jensen's Inequality）

对于凸函数 \\(f\\) 和实数权重 \\(a_i \geq 0\\) 满足 \\(\sum a_i = 1\\)，有：

\\[
f\left(\sum_{i=1}^n a_i x_i\right) \leq \sum_{i=1}^n a_i f(x_i)
\\]

## 3. 组合数学

## 4. 复变基础