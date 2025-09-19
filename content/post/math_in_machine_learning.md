---
date: '2025-03-19T20:17:16+08:00'
draft: false
title: '机器学习&深度学习数学基础'
categories:
  - AI
  - math
keywords:
  - machine learning
tags:
  - machine learning
mathjax: true
---

# 线性代数

线性代数是机器学习的数学基础，为数据表示和算法实现提供了核心工具。深入理解线性代数原理对于掌握现代机器学习算法至关重要。

## 核心概念与数学原理

### 向量空间与线性变换

**定义**：向量空间V是满足以下公理的集合，配备加法和标量乘法运算：
- 加法交换律：$u + v = v + u$
- 加法结合律：$(u + v) + w = u + (v + w)$
- 零向量存在：$\exists 0 \in V$ 使得 $v + 0 = v$
- 逆元存在：$\forall v \in V, \exists -v \in V$ 使得 $v + (-v) = 0$

**线性变换**：映射 $T: V \rightarrow W$ 满足：
$$T(\alpha u + \beta v) = \alpha T(u) + \beta T(v)$$

**矩阵表示**：每个线性变换 $T: \mathbb{R}^n \rightarrow \mathbb{R}^m$ 都对应唯一的矩阵 $A \in \mathbb{R}^{m\times n}$ 使得：
$$T(x) = Ax$$

### 内积空间与正交性

**内积定义**：函数 $\langle \cdot, \cdot \rangle: V \times V \rightarrow \mathbb{R}$ 满足：
- 正定性：$\langle v, v \rangle \geq 0$ 且 $\langle v, v \rangle = 0 \Leftrightarrow v = 0$
- 对称性：$\langle u, v \rangle = \langle v, u \rangle$
- 线性性：$\langle \alpha u + \beta v, w \rangle = \alpha \langle u, w \rangle + \beta \langle v, w \rangle$

**柯西-施瓦茨不等式**：
$$|\langle u, v \rangle| \leq \|u\| \cdot \|v\|$$
其中 $\|v\| = \sqrt{\langle v, v \rangle}$ 是诱导范数。

### 特征值分解与对角化

**特征值与特征向量**：对于方阵 $A \in \mathbb{R}^{n\times n}$，若存在非零向量 $v \in \mathbb{R}^n$ 和标量 $\lambda \in \mathbb{R}$ 使得：
$$Av = \lambda v$$
则称 $\lambda$ 为特征值，$v$ 为对应的特征向量。

**特征分解定理**：若 $A \in \mathbb{R}^{n\times n}$ 有 $n$ 个线性无关的特征向量，则：
$$A = V\Lambda V^{-1}$$
其中 $V = [v_1, v_2, \ldots, v_n]$ 是特征向量矩阵，$\Lambda = \text{diag}(\lambda_1, \lambda_2, \ldots, \lambda_n)$ 是特征值对角矩阵。

**谱定理**：对于实对称矩阵 $A = A^T$，存在正交矩阵 $Q$（即 $Q^T Q = I$）使得：
$$A = Q\Lambda Q^T$$
其中 $\Lambda$ 包含实特征值，$Q$ 的列是对应的正交特征向量。

### 奇异值分解(SVD)

**定理**：任意矩阵 $A \in \mathbb{R}^{m\times n}$ 都可分解为：
$$A = U\Sigma V^T$$
其中：
- $U \in \mathbb{R}^{m\times m}$ 是正交矩阵（左奇异向量）
- $V \in \mathbb{R}^{n\times n}$ 是正交矩阵（右奇异向量）
- $\Sigma \in \mathbb{R}^{m\times n}$ 是对角矩阵，对角线元素 $\sigma_1 \geq \sigma_2 \geq \cdots \geq \sigma_{\min(m,n)} \geq 0$ 称为奇异值

**与特征值的关系**：$A^T A = V\Sigma^T\Sigma V^T$ 和 $AA^T = U\Sigma\Sigma^T U^T$，即：
- $A^T A$ 的特征值是奇异值的平方：$\lambda_i(A^T A) = \sigma_i^2$
- $V$ 的列是 $A^T A$ 的特征向量
- $U$ 的列是 $AA^T$ 的特征向量

### 矩阵范数与条件数

**弗罗贝尼乌斯范数**：
$$\|A\|_F = \sqrt{\sum_{i=1}^m \sum_{j=1}^n |a_{ij}|^2} = \sqrt{\text{tr}(A^T A)} = \sqrt{\sum_{i=1}^{\min(m,n)} \sigma_i^2}$$

**谱范数**（2-范数）：
$$\|A\|_2 = \sup_{x \neq 0} \frac{\|Ax\|_2}{\|x\|_2} = \sigma_{\max}(A)$$

**条件数**：
$$\kappa(A) = \|A\|_2 \cdot \|A^{-1}\|_2 = \frac{\sigma_{\max}(A)}{\sigma_{\min}(A)}$$
条件数衡量矩阵求逆的数值稳定性，条件数越大，矩阵越接近奇异。

## 机器学习中的数学应用

### 主成分分析(PCA)的数学推导

给定数据中心化矩阵 $X \in \mathbb{R}^{n\times d}$，PCA求解以下优化问题：
$$\max_{w \in \mathbb{R}^d} w^T X^T X w \quad \text{s.t.} \quad \|w\|_2 = 1$$

**拉格朗日函数**：
$$\mathcal{L}(w, \lambda) = w^T X^T X w - \lambda(w^T w - 1)$$

**KKT条件**：
$$\nabla_w \mathcal{L} = 2X^T X w - 2\lambda w = 0 \Rightarrow X^T X w = \lambda w$$

这表明最优的 $w$ 是 $X^T X$ 的特征向量，对应的特征值 $\lambda$ 表示该方向上的方差。

**主成分**：第 $k$ 个主成分是 $X^T X$ 的第 $k$ 大特征值对应的特征向量，解释的方差比例为：
$$\text{解释方差比例} = \frac{\lambda_k}{\sum_{i=1}^d \lambda_i}$$

### 线性回归的正规方程

对于线性模型 $y = Xw + \epsilon$，最小二乘估计最小化：
$$L(w) = \|y - Xw\|_2^2 = (y - Xw)^T(y - Xw)$$

**梯度计算**：
$$\nabla_w L(w) = -2X^T(y - Xw)$$

**正规方程**：
$$X^T X w = X^T y \Rightarrow w = (X^T X)^{-1} X^T y$$

**几何解释**：最小二乘解使得预测向量 $Xw$ 是 $y$ 在 $X$ 列空间上的正交投影：
$$Xw = P_X y = X(X^T X)^{-1} X^T y$$
其中 $P_X = X(X^T X)^{-1} X^T$ 是投影矩阵。

### 岭回归的数学分析

岭回归最小化带L2正则化的目标函数：
$$L_{\text{ridge}}(w) = \|y - Xw\|_2^2 + \lambda \|w\|_2^2$$

**解析解**：
$$\hat{w}_{\text{ridge}} = (X^T X + \lambda I)^{-1} X^T y$$

**偏差-方差权衡**：
- **偏差**：$\text{Bias}(\hat{w}_{\text{ridge}}) = -\lambda (X^T X + \lambda I)^{-1} w^*$
- **方差**：$\text{Var}(\hat{w}_{\text{ridge}}) = \sigma^2 (X^T X + \lambda I)^{-1} X^T X (X^T X + \lambda I)^{-1}$

**奇异值分析**：利用SVD $X = U\Sigma V^T$，岭回归解可表示为：
$$\hat{w}_{\text{ridge}} = V (\Sigma^T \Sigma + \lambda I)^{-1} \Sigma^T U^T y = \sum_{i=1}^d \frac{\sigma_i}{\sigma_i^2 + \lambda} (u_i^T y) v_i$$

相比普通最小二乘 $\hat{w}_{\text{OLS}} = \sum_{i=1}^d \frac{1}{\sigma_i} (u_i^T y) v_i$，岭回归通过因子 $\frac{\sigma_i^2}{\sigma_i^2 + \lambda}$ 收缩小奇异值对应的成分，提高数值稳定性。

### 神经网络前向传播的矩阵表示

对于L层神经网络，第$l$层的计算为：
$$Z^{[l]} = W^{[l]} A^{[l-1]} + b^{[l]}$$
$$A^{[l]} = g^{[l]}(Z^{[l]})$$

其中：
- $A^{[0]} = X \in \mathbb{R}^{n\times d}$ 是输入矩阵
- $W^{[l]} \in \mathbb{R}^{n_l \times n_{l-1}}$ 是权重矩阵
- $b^{[l]} \in \mathbb{R}^{n_l}$ 是偏置向量
- $g^{[l]}$ 是激活函数

**批量处理**：矩阵形式允许同时处理整个批次，充分利用GPU并行计算能力。对于批次大小为$m$的训练：
$$Z^{[l]} = W^{[l]} A^{[l-1]} + b^{[l]} \mathbf{1}_m^T$$
其中 $\mathbf{1}_m \in \mathbb{R}^m$ 是全1向量，通过广播机制实现偏置的批量添加。

# 概率论&统计

概率论和统计学为机器学习提供了处理不确定性和从数据中学习的基础框架。现代机器学习算法的理论基础深深植根于概率统计的数学原理中。

## 概率论的数学基础

### 概率空间与测度论

**概率空间三元组** $(\Omega, \mathcal{F}, P)$：
- **样本空间** $\Omega$：所有可能结果的集合
- **事件域** $\mathcal{F}$：$\Omega$ 子集的 $\sigma$-代数，满足：
  1. $\Omega \in \mathcal{F}$
  2. 若 $A \in \mathcal{F}$，则 $A^c \in \mathcal{F}$（对补集封闭）
  3. 若 $A_i \in \mathcal{F}$（$i = 1,2,\ldots$），则 $\bigcup_{i=1}^{\infty} A_i \in \mathcal{F}$（对可数并封闭）
- **概率测度** $P: \mathcal{F} \rightarrow [0,1]$，满足：
  1. $P(\Omega) = 1$（规范性）
  2. 若 $A_i \cap A_j = \emptyset$（$i \neq j$），则 $P(\bigcup_{i=1}^{\infty} A_i) = \sum_{i=1}^{\infty} P(A_i)$（可数可加性）

**条件概率**：对于 $P(B) > 0$：
$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

**乘法法则**：
$$P(A \cap B) = P(A|B)P(B) = P(B|A)P(A)$$

### 随机变量与分布函数

**随机变量**：可测函数 $X: \Omega \rightarrow \mathbb{R}$，满足对任意 Borel 集 $B \subseteq \mathbb{R}$，有 $X^{-1}(B) \in \mathcal{F}$。

**累积分布函数(CDF)**：
$$F_X(x) = P(X \leq x) = P(\{\omega \in \Omega: X(\omega) \leq x\})$$

**性质**：
1. 单调不减：$x_1 \leq x_2 \Rightarrow F_X(x_1) \leq F_X(x_2)$
2. 右连续：$\lim_{x \to a^+} F_X(x) = F_X(a)$
3. 极限性质：$\lim_{x \to -\infty} F_X(x) = 0$，$\lim_{x \to +\infty} F_X(x) = 1$

**概率密度函数(PDF)**：对于连续随机变量，若存在非负函数 $f_X(x)$ 使得：
$$F_X(x) = \int_{-\infty}^x f_X(t) dt$$
则 $f_X(x) = \frac{d}{dx} F_X(x)$（在可微点处）。

### 期望与方差的数学理论

**期望（勒贝格积分定义）**：
$$E[X] = \int_{\Omega} X(\omega) dP(\omega) = \int_{-\infty}^{+\infty} x dF_X(x)$$

**方差**：
$$\text{Var}(X) = E[(X - E[X])^2] = E[X^2] - (E[X])^2$$

**矩生成函数(MGF)**：
$$M_X(t) = E[e^{tX}] = \int_{-\infty}^{+\infty} e^{tx} dF_X(x)$$

**性质**：若 $M_X(t)$ 在 $t=0$ 的某邻域内存在，则：
$$E[X^n] = M_X^{(n)}(0) = \left. \frac{d^n}{dt^n} M_X(t) \right|_{t=0}$$

### 重要概率分布的数学理论

**多元高斯分布**：随机向量 $X \in \mathbb{R}^d$ 服从多元高斯分布 $N(\mu, \Sigma)$，其PDF为：
$$f_X(x) = \frac{1}{(2\pi)^{d/2} |\Sigma|^{1/2}} \exp\left\{-\frac{1}{2}(x-\mu)^T \Sigma^{-1} (x-\mu)\right\}$$

**性质**：
1. 线性变换：若 $X \sim N(\mu, \Sigma)$，则 $AX + b \sim N(A\mu + b, A\Sigma A^T)$
2. 条件分布：对于分块高斯向量 $\begin{pmatrix} X_1 \\ X_2 \end{pmatrix} \sim N\left(\begin{pmatrix} \mu_1 \\ \mu_2 \end{pmatrix}, \begin{pmatrix} \Sigma_{11} & \Sigma_{12} \\ \Sigma_{21} & \Sigma_{22} \end{pmatrix}\right)$：
   $$X_1 | X_2 = x_2 \sim N(\mu_1 + \Sigma_{12}\Sigma_{22}^{-1}(x_2 - \mu_2), \Sigma_{11} - \Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21})$$

**指数族分布**：
$$f(x|\theta) = h(x) \exp\left\{\eta(\theta)^T T(x) - A(\theta)\right\}$$
其中 $\eta(\theta)$ 是自然参数，$T(x)$ 是充分统计量，$A(\theta)$ 是对数配分函数。

**性质**：指数族分布具有共轭先验，后验分布与先验分布属于同一族。

### 大数定律与中心极限定理

**强大数定律**：设 $\{X_n\}$ 是i.i.d.随机变量序列，$E[X_1] = \mu$，则：
$$P\left(\lim_{n \to \infty} \frac{1}{n} \sum_{i=1}^n X_i = \mu\right) = 1$$

**中心极限定理(CLT)**：设 $\{X_n\}$ 是i.i.d.随机变量序列，$E[X_1] = \mu$，$\text{Var}(X_1) = \sigma^2 \in (0, \infty)$，则：
$$\sqrt{n}\left(\frac{1}{n} \sum_{i=1}^n X_i - \mu\right) \xrightarrow{d} N(0, \sigma^2)$$
其中 $\xrightarrow{d}$ 表示依分布收敛。

## 统计推断的数学理论

### 参数估计理论

**最大似然估计(MLE)**：对于观测数据 $X = (x_1, \ldots, x_n)$，MLE求解：
$$\hat{\theta}_{\text{MLE}} = \arg\max_{\theta \in \Theta} L(\theta|X) = \arg\max_{\theta \in \Theta} \prod_{i=1}^n f(x_i|\theta)$$

**渐近性质**：在正则条件下，MLE具有：
1. **一致性**：$\hat{\theta}_{\text{MLE}} \xrightarrow{p} \theta_0$（依概率收敛到真值）
2. **渐近正态性**：$\sqrt{n}(\hat{\theta}_{\text{MLE}} - \theta_0) \xrightarrow{d} N(0, I(\theta_0)^{-1})$
3. **有效性**：达到Cramér-Rao下界

**Fisher信息矩阵**：
$$I(\theta) = -E\left[\frac{\partial^2}{\partial \theta \partial \theta^T} \log f(X|\theta)\right] = E\left[\left(\frac{\partial}{\partial \theta} \log f(X|\theta)\right)\left(\frac{\partial}{\partial \theta} \log f(X|\theta)\right)^T\right]$$

**Cramér-Rao下界**：对于无偏估计量 $\hat{\theta}$，有：
$$\text{Var}(\hat{\theta}) \geq \frac{1}{n} I(\theta)^{-1}$$

### 贝叶斯推断理论

**贝叶斯定理**：
$$p(\theta|X) = \frac{p(X|\theta) p(\theta)}{p(X)} = \frac{p(X|\theta) p(\theta)}{\int p(X|\theta') p(\theta') d\theta'}$$

**后验预测分布**：
$$p(x_{\text{new}}|X) = \int p(x_{\text{new}}|\theta) p(\theta|X) d\theta$$

**共轭先验**：若先验分布 $p(\theta)$ 与似然函数 $p(X|\theta)$ 共轭，则后验分布 $p(\theta|X)$ 与先验分布属于同一族。

**例子**：
- 高斯似然 + 高斯先验 → 高斯后验
- 伯努利似然 + Beta先验 → Beta后验
- 多项式似然 + Dirichlet先验 → Dirichlet后验

### 假设检验的数学理论

**Neyman-Pearson引理**：对于简单假设检验 $H_0: \theta = \theta_0$ vs $H_1: \theta = \theta_1$，似然比检验：
$$\Lambda(X) = \frac{L(\theta_0|X)}{L(\theta_1|X)}$$
是最优势检验。

**p值定义**：
$$p\text{-value} = P_{H_0}(T(X) \geq T_{\text{obs}})$$
其中 $T(X)$ 是检验统计量，$T_{\text{obs}}$ 是观测值。

## 机器学习中的概率统计应用

### 高斯混合模型(GMM)的EM算法

**模型**：$p(x) = \sum_{k=1}^K \pi_k N(x|\mu_k, \Sigma_k)$，其中 $\sum_{k=1}^K \pi_k = 1$。

**完全数据对数似然**：
$$\log p(X, Z|\theta) = \sum_{i=1}^n \sum_{k=1}^K z_{ik} \log\left[\pi_k N(x_i|\mu_k, \Sigma_k)\right]$$

**EM算法**：
1. **E步**（期望）：
   $$\gamma_{ik} = E[z_{ik}|x_i, \theta^{(t)}] = \frac{\pi_k^{(t)} N(x_i|\mu_k^{(t)}, \Sigma_k^{(t)})}{\sum_{j=1}^K \pi_j^{(t)} N(x_i|\mu_j^{(t)}, \Sigma_j^{(t)})}$$

2. **M步**（最大化）：
   $$\pi_k^{(t+1)} = \frac{1}{n} \sum_{i=1}^n \gamma_{ik}$$
   $$\mu_k^{(t+1)} = \frac{\sum_{i=1}^n \gamma_{ik} x_i}{\sum_{i=1}^n \gamma_{ik}}$$
   $$\Sigma_k^{(t+1)} = \frac{\sum_{i=1}^n \gamma_{ik} (x_i - \mu_k^{(t+1)})(x_i - \mu_k^{(t+1)})^T}{\sum_{i=1}^n \gamma_{ik}}$$

**收敛性**：EM算法保证似然函数单调不减，收敛到局部极大值。

### 逻辑回归的统计性质

**模型**：对于二分类问题，$p(y=1|x) = \sigma(w^T x) = \frac{1}{1 + e^{-w^T x}}$。

**对数似然函数**：
$$\ell(w) = \sum_{i=1}^n \left[y_i \log \sigma(w^T x_i) + (1-y_i) \log (1-\sigma(w^T x_i))\right]$$

**梯度**：
$$\nabla_w \ell(w) = \sum_{i=1}^n (y_i - \sigma(w^T x_i)) x_i = X^T(y - \hat{y})$$

**海森矩阵**：
$$H = \nabla_w^2 \ell(w) = -\sum_{i=1}^n \sigma(w^T x_i)(1-\sigma(w^T x_i)) x_i x_i^T = -X^T S X$$
其中 $S = \text{diag}(\sigma(w^T x_i)(1-\sigma(w^T x_i)))$。

**渐近分布**：
$$\hat{w} \approx N(w^*, (X^T S X)^{-1})$$

### 信息论与机器学习

**熵**：随机变量 $X$ 的不确定性度量
$$H(X) = -\sum_x p(x) \log p(x)$$

**条件熵**：
$$H(Y|X) = \sum_x p(x) H(Y|X=x) = -\sum_{x,y} p(x,y) \log p(y|x)$$

**互信息**：两个随机变量的相互依赖程度
$$I(X;Y) = H(Y) - H(Y|X) = H(X) - H(X|Y) = \sum_{x,y} p(x,y) \log \frac{p(x,y)}{p(x)p(y)}$$

**KL散度**：两个概率分布的差异度量
$$D_{KL}(P\|Q) = \sum_x p(x) \log \frac{p(x)}{q(x)} = E_P\left[\log \frac{p(X)}{q(X)}\right]$$

**性质**：
1. $D_{KL}(P\|Q) \geq 0$（吉布斯不等式）
2. $D_{KL}(P\|Q) = 0 \Leftrightarrow P = Q$
3. 不满足对称性和三角不等式

**交叉熵**：
$$H(P,Q) = -\sum_x p(x) \log q(x) = H(P) + D_{KL}(P\|Q)$$

**与机器学习的关系**：
- 逻辑回归的负对数似然 = 交叉熵损失
- 决策树的划分准则（信息增益）基于互信息
- 变分推断最小化KL散度
- 生成对抗网络(GAN)最小化JS散度

# 微积分

微积分为机器学习提供了优化算法和模型训练的理论基础，特别是在梯度计算和参数更新方面。现代深度学习算法的核心数学工具都建立在严格的微积分理论之上。

## 多元微积分的数学理论

### 梯度与方向导数

**梯度定义**：对于函数 $f: \mathbb{R}^n \rightarrow \mathbb{R}$，在点 $x \in \mathbb{R}^n$ 处的梯度为：
$$\nabla f(x) = \left[\frac{\partial f}{\partial x_1}(x), \frac{\partial f}{\partial x_2}(x), \ldots, \frac{\partial f}{\partial x_n}(x)\right]^T$$

**方向导数**：沿单位向量 $v \in \mathbb{R}^n$ 的方向导数为：
$$D_v f(x) = \lim_{t \to 0} \frac{f(x + tv) - f(x)}{t} = \nabla f(x)^T v$$

**几何意义**：梯度 $\nabla f(x)$ 指向函数值增长最快的方向，其模长表示增长率：
$$\max_{\|v\|_2 = 1} D_v f(x) = \|\nabla f(x)\|_2$$

### 雅可比矩阵与链式法则

**雅可比矩阵**：对于向量值函数 $f: \mathbb{R}^n \rightarrow \mathbb{R}^m$，其雅可比矩阵为：
$$J_f(x) = \begin{bmatrix}
\frac{\partial f_1}{\partial x_1}(x) & \frac{\partial f_1}{\partial x_2}(x) & \cdots & \frac{\partial f_1}{\partial x_n}(x) \\
\frac{\partial f_2}{\partial x_1}(x) & \frac{\partial f_2}{\partial x_2}(x) & \cdots & \frac{\partial f_2}{\partial x_n}(x) \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial f_m}{\partial x_1}(x) & \frac{\partial f_m}{\partial x_2}(x) & \cdots & \frac{\partial f_m}{\partial x_n}(x)
\end{bmatrix} \in \mathbb{R}^{m\times n}$$

**链式法则**：若 $g: \mathbb{R}^n \rightarrow \mathbb{R}^m$，$f: \mathbb{R}^m \rightarrow \mathbb{R}^p$，则复合函数 $h = f \circ g: \mathbb{R}^n \rightarrow \mathbb{R}^p$ 的雅可比矩阵为：
$$J_h(x) = J_f(g(x)) \cdot J_g(x)$$

**神经网络中的应用**：对于 $L$ 层网络 $f = f_L \circ f_{L-1} \circ \cdots \circ f_1$，反向传播算法基于：
$$J_f(x) = J_{f_L}(f_{L-1}(\cdots f_1(x))) \cdot J_{f_{L-1}}(f_{L-2}(\cdots f_1(x))) \cdots J_{f_1}(x)$$

### 海森矩阵与二阶条件

**海森矩阵**：对于函数 $f: \mathbb{R}^n \rightarrow \mathbb{R}$，其海森矩阵为二阶偏导数矩阵：
$$H_f(x) = \nabla^2 f(x) = \begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2}(x) & \frac{\partial^2 f}{\partial x_1 \partial x_2}(x) & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n}(x) \\
\frac{\partial^2 f}{\partial x_2 \partial x_1}(x) & \frac{\partial^2 f}{\partial x_2^2}(x) & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n}(x) \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1}(x) & \frac{\partial^2 f}{\partial x_n \partial x_2}(x) & \cdots & \frac{\partial^2 f}{\partial x_n^2}(x)
\end{bmatrix}$$

**泰勒展开**：函数 $f$ 在点 $x$ 附近的二阶泰勒展开为：
$$f(x + h) = f(x) + \nabla f(x)^T h + \frac{1}{2} h^T H_f(x) h + o(\|h\|_2^2)$$

**极值条件**：对于可微函数 $f$，若 $x^*$ 是局部极小值点，则：
1. **一阶必要条件**：$\nabla f(x^*) = 0$
2. **二阶必要条件**：$H_f(x^*)$ 是半正定矩阵
3. **二阶充分条件**：若 $\nabla f(x^*) = 0$ 且 $H_f(x^*)$ 正定，则 $x^*$ 是严格局部极小值点

### 凸分析基础

**凸集**：集合 $C \subseteq \mathbb{R}^n$ 是凸集，如果对于任意 $x, y \in C$ 和 $\lambda \in [0, 1]$，有：
$$\lambda x + (1 - \lambda) y \in C$$

**凸函数**：函数 $f: C \rightarrow \mathbb{R}$ 是凸函数，如果对于任意 $x, y \in C$ 和 $\lambda \in [0, 1]$，有：
$$f(\lambda x + (1 - \lambda) y) \leq \lambda f(x) + (1 - \lambda) f(y)$$

**判别条件**：对于二次可微函数 $f$，以下等价：
1. $f$ 是凸函数
2. 海森矩阵 $H_f(x)$ 对所有 $x \in C$ 半正定
3. 对任意 $x, y \in C$：$f(y) \geq f(x) + \nabla f(x)^T(y - x)$

**强凸性**：函数 $f$ 是 $\mu$-强凸的，如果存在 $\mu > 0$ 使得：
$$f(y) \geq f(x) + \nabla f(x)^T(y - x) + \frac{\mu}{2}\|y - x\|_2^2$$
等价于：$H_f(x) \succeq \mu I$（海森矩阵的最小特征值 $\geq \mu$）

## 优化算法的数学分析

### 梯度下降的收敛性分析

**L-光滑性**：函数 $f$ 是 $L$-光滑的，如果其梯度是 $L$-Lipschitz连续的：
$$\|\nabla f(x) - \nabla f(y)\|_2 \leq L\|x - y\|_2, \quad \forall x, y$$

等价于：$f(y) \leq f(x) + \nabla f(x)^T(y - x) + \frac{L}{2}\|y - x\|_2^2$

**收敛定理**：对于凸且 $L$-光滑的函数 $f$，梯度下降：
$$x_{t+1} = x_t - \eta \nabla f(x_t)$$

当步长 $\eta \leq \frac{1}{L}$ 时，有：
$$f(x_T) - f(x^*) \leq \frac{\|x_0 - x^*\|_2^2}{2\eta T}$$

**强凸函数的线性收敛**：若 $f$ 还是 $\mu$-强凸的，则：
$$\|x_{t+1} - x^*\|_2^2 \leq (1 - \eta\mu)\|x_t - x^*\|_2^2$$

收敛速度为线性：$O((1 - \frac{\mu}{L})^t)$，条件数 $\kappa = \frac{L}{\mu}$ 决定收敛快慢。

### 随机梯度下降的方差分析

**SGD更新**：$x_{t+1} = x_t - \eta_t g_t$，其中 $g_t$ 是 $\nabla f(x_t)$ 的无偏估计：$E[g_t] = \nabla f(x_t)$

**方差分解**：
$$E[\|g_t\|_2^2] = \|\nabla f(x_t)\|_2^2 + \text{Var}(g_t)$$

**收敛条件**：对于凸函数，若步长满足 $\sum_{t=1}^{\infty} \eta_t = \infty$ 且 $\sum_{t=1}^{\infty} \eta_t^2 < \infty$，则SGD收敛到最优解。

**方差缩减技术**：
- **SVRG**：利用全梯度减少方差
- **SAGA**：存储历史梯度信息
- **SARAH**：递归梯度估计

### 牛顿法的二次收敛

**牛顿更新**：$x_{t+1} = x_t - H_f(x_t)^{-1} \nabla f(x_t)$

**局部二次收敛**：在标准假设下，当初始点 $x_0$ 足够接近最优解 $x^*$ 时，有：
$$\|x_{t+1} - x^*\|_2 \leq C\|x_t - x^*\|_2^2$$

**自协调性**：对于自协调函数，牛顿法具有全局多项式时间复杂度。

### 约束优化的KKT条件

**拉格朗日函数**：对于约束优化问题：
$$\min_x f(x) \quad \text{s.t.} \quad g_i(x) \leq 0, h_j(x) = 0$$

拉格朗日函数为：
$$\mathcal{L}(x, \lambda, \nu) = f(x) + \sum_i \lambda_i g_i(x) + \sum_j \nu_j h_j(x)$$

**KKT条件**：若 $x^*$ 是局部最优解，且满足约束规范条件，则存在拉格朗日乘子 $\lambda^*, \nu^*$ 使得：
1. **平稳性**：$\nabla_x \mathcal{L}(x^*, \lambda^*, \nu^*) = 0$
2. **原始可行性**：$g_i(x^*) \leq 0, h_j(x^*) = 0$
3. **对偶可行性**：$\lambda_i^* \geq 0$
4. **互补松弛性**：$\lambda_i^* g_i(x^*) = 0$

## 深度学习中的高级优化理论

### 反向传播的数学推导

**计算图**：神经网络表示为复合函数 $f = f_L \circ \cdots \circ f_1$，每个节点计算：
$$z_l = W_l a_{l-1} + b_l, \quad a_l = \sigma_l(z_l)$$

**前向传播**：从输入到输出的计算过程：
$$\frac{\partial z_l}{\partial a_{l-1}} = W_l, \quad \frac{\partial a_l}{\partial z_l} = \text{diag}(\sigma_l'(z_l))$$

**反向传播**：基于链式法则的梯度反向传递：
$$\delta_l = \frac{\partial L}{\partial z_l} = \left(\frac{\partial z_{l+1}}{\partial a_l}\right)^T \frac{\partial L}{\partial z_{l+1}} = (W_{l+1}^T \delta_{l+1}) \circ \sigma_l'(z_l)$$

其中 $\circ$ 表示逐元素乘法。

**参数梯度**：
$$\frac{\partial L}{\partial W_l} = \delta_l a_{l-1}^T, \quad \frac{\partial L}{\partial b_l} = \delta_l$$

### 自适应学习率方法的数学原理

**AdaGrad**：累积平方梯度：
$$G_t = G_{t-1} + g_t \circ g_t, \quad x_{t+1} = x_t - \frac{\eta}{\sqrt{G_t + \epsilon}} \circ g_t$$

**RMSprop**：指数移动平均：
$$E_t = \beta E_{t-1} + (1 - \beta) g_t \circ g_t, \quad x_{t+1} = x_t - \frac{\eta}{\sqrt{E_t + \epsilon}} \circ g_t$$

**Adam**：结合动量和二阶矩估计：
$$\begin{aligned}
m_t &= \beta_1 m_{t-1} + (1 - \beta_1) g_t \\
v_t &= \beta_2 v_{t-1} + (1 - \beta_2) g_t \circ g_t \\
\hat{m}_t &= \frac{m_t}{1 - \beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1 - \beta_2^t} \\
x_{t+1} &= x_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \circ \hat{m}_t
\end{aligned}$$

### 现代优化技术

**自然梯度法**：考虑参数空间的几何结构，使用Fisher信息矩阵：
$$x_{t+1} = x_t - \eta F(x_t)^{-1} \nabla f(x_t)$$

**二阶方法的近似**：
- **拟牛顿法**：BFGS、L-BFGS近似海森矩阵
- **信赖域方法**：在局部区域内近似模型
- **立方正则化**：使用三阶导数信息

**随机优化的理论发展**：
- **非凸优化的收敛性**：逃离鞍点和局部极小值
- **过参数化模型的隐式正则化**：神经网络的特殊优化性质
- **梯度流和平均化**：连续时间极限分析


