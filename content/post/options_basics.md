---
date: '2025-06-02T09:07:36+08:00'
draft: false
title: '期权基础知识'
categories:
  - quantitive
keywords:
  - options
  - black-scholes
tags:
  - options
  - black-scholes
mathjax: true
---

# 期权基础

期权是一种金融合约，赋予持有者在特定日期或之前以预定价格买入或卖出标的资产的权利（但非义务）。期权买方支付权利金获得这项权利，卖方收取权利金并承担相应义务。

## 一些基本概念

1. 认购/认沽期权
    - 认购期权：也叫看涨期权Call, 买方有权以约定价格购买指定资产。
    - 认沽期权：也就看跌期权Put, 买方有权以约定价格出售指定资产。
2. 权利金/执行价
    - 权利金：期权合约的购买价格。
    - 执行价：期权到期时，资产的市场价格。
3. 欧式期权/美式期权
    - 欧式期权：仅期权合约规定的到期日当天行权，常见于股票指数期权、外汇期权等，定价模型相对简单
    - 美式期权：到期日或之前任何一天都可以行权，常见于个股期权，ETF期权等，定价复杂


## 期权合约要素

期权合约要素包含到期日Expiration date、到期月份、交割方式、行权价格strike price、合约单位contract unit、权利金premium等。

根据执行价格与与标的资产市场价格的关系，期权可以分为三种状态。实值/平值/虚值期权：
- 实值期权：(In-the-Money,ITM)立即行权能够产生正收益的期权，对于看涨期权即标的现价>执行价格，对于看跌期权，就是标的现价<执行价格
- 平值期权：(At-the-Money,ATM)执行价格≈标的现价的期权，通常指执行价格最接近标的现价的期权。有时将执行价格±1-2%范围内的都视为平值
- 虚值期权：(Out-of-the-Money,OTM)立即行权无利可图的期权。对于看涨期权即标的现价<执行价格，对于看跌期权，就是标的现价>执行价格

期权的价值由内在价值与时间价值构成。内在价值即买方立刻行权获得的收入，时间价值即到期后到期日内在价值的折现值。时间价值通常呈现抛物线加速衰减的情况。

期权价格最重要的三个影响因素：标的资产价格、时间和波动率。

# 常见期权策略

## 单腿策略

单只期权策略主要包括：买入认购/认沽期权，卖出认购/认沽期权。其中买入认购、卖出认沽是看涨型策略，买入认沽、卖出认购是看跌型策略。

> 简单来说：看大涨买认购，看大跌买认沽；不看涨卖认购，不看跌卖认沽。

### 盈亏曲线

假设某公司股价为50元，则不同操作的盈亏曲线对应如下

1. 买入看涨期权

买入行权价 52 元的看涨期权的价格是 2 元，则盈亏曲线如下

![single-buy-call](/images/quantitive/single-buy-call.jpg)

2. 卖出看涨期权

与买入的刚好上下对称，因为互为对手盘

![single-sell-call](/images/quantitive/single-sell-call.jpg)

3. 买入看空期权

如果我们买入一个 48 元的期权，期权价格是 2 元。

![single-buy-put](/images/quantitive/single-buy-put.jpg)

4. 卖出看空期权

同样，卖出看跌期权的盈亏曲线和买入的刚好上下对称，因为两者互为对手盘。

![single-sell-put](/images/quantitive/single-sell-put.jpg)


### 期权买方和卖方的风险

期权买方的风险：
1. 价值归零风险：指期权到期时，内在价值为0，一般来说持有到期是比较少的，可以设置一个止损线来避免归0风险。
2. 高溢价风险：虚值期权到期日价值一定会归0
3. 流动性风险：指期权合约的买卖双方数量不平衡，导致买卖双方无法及时成交，从而增加了交易成本。
4. 行权交割风险：错过行权，或者对于认购期权的买方，如果在T日行权，必须T+1日才能得到券，T+2日才能卖出，会带来两天的价格波动风险。

期权卖方需要考虑的核心要素：
1. 波动率：资产价格的波动程度，是期权定价的重要因素。一个很经典的策略就是：**卖出高隐含波动率的期权，买入对应数量隐含波动率正常的合约**，赚取波动率的价差收入
2. 流动性：衡量流动性的两个重要因素：买卖价差与盘口的报价数量
3. 自身的风险承受能力：首先期权买方的收益有限，但损失无限，所以止损是非常必要的，常见的有固定价位止损、技术指标止损等；其次期权卖方需要足额保证金，不可满仓操作。

> 1. 期权卖方建议：（1）多卖隐含波动率过度偏离的期权（例如高于根据波动率测算的期权理论价值25%以上的）（2）尽量多卖虚值期权
> 2. 期权卖方一定要关注保证金风险，以上交所股票期权为例，保证金分为开仓保证金和维持保证金。

## 保险策略


# 波动率

波动率是衡量资产价格变动幅度的统计指标，通常用标准差表示。它反映了资产价格的波动程度，波动率越大，资产价格的不确定性越高。

## 历史波动率

# Black-Scholes 模型

Black-Scholes 模型是期权定价的最基本模型，由1973年由 Fischer Black 和 Myron Scholes 提出。Robert Merton同年对其进行了重要扩展。该模型为欧式期权提供了理论定价框架，开创了现代金融衍生品定价的新纪元。

## 模型基本假设

1. 市场无摩擦（无交易成本、无税收）
2. 允许无限制卖空
3. 无风险利率r已知且恒定
4. 标的资产价格**服从几何布朗运动Geometric Brownian Motion**，即服从对数正态分布
5. 标的资产不支付股息
6. 期权是欧式的（仅能在到期日执行）
7. 市场无套利机会

## 二、基本假设

Black-Scholes模型基于以下几个关键假设：

1. **标的资产价格服从几何布朗运动（Geometric Brownian Motion）**：
   \[
   dS_t = \mu S_t dt + \sigma S_t dW_t
   \]
   其中：
   - \(S_t\) 是时间 \(t\) 时的标的资产价格
   - \(\mu\) 是资产的期望收益率（漂移率）
   - \(\sigma\) 是资产价格的波动率（标准差）
   - \(W_t\) 是标准布朗运动（Wiener过程）

2. **无套利市场**：不存在无风险套利机会。

3. **无风险利率 \(r\) 是常数**，且可以连续复利。

4. **标的资产不支付股息**（原始模型假设）。

5. **市场是完美的**：没有交易费用、没有税收、可以无限分割资产。

6. **期权是欧式期权**，只能在到期日行权。

---

## 三、建模过程与推导

### 1. 标的资产价格的随机过程

假设标的资产价格 $S_t$ 服从几何布朗运动：
$$
dS_t = \mu S_t dt + \sigma S_t dW_t
$$

其中 $dW_t$ 是布朗运动的增量，满足：
$$
E[dW_t] = 0, \quad Var(dW_t) = dt
$$

### 2. 期权价格函数

定义期权价格为 $V(S,t)$，是标的资产价格和时间的函数。我们的目标是求出 $V$。

### 3. 应用伊藤引理（Itô's Lemma）

对 $V(S,t)$ 应用伊藤引理：
$$
dV = \frac{\partial V}{\partial t} dt + \frac{\partial V}{\partial S} dS + \frac{1}{2} \frac{\partial^2 V}{\partial S^2} (dS)^2
$$

注意到：
$$
(dS)^2 = (\sigma S dW_t)^2 = \sigma^2 S^2 dt
$$
因为 $dW_t^2 = dt$。

代入 $dS$：
$$
dV = \frac{\partial V}{\partial t} dt + \frac{\partial V}{\partial S} (\mu S dt + \sigma S dW_t) + \frac{1}{2} \frac{\partial^2 V}{\partial S^2} \sigma^2 S^2 dt
$$

整理：
$$
dV = \left( \frac{\partial V}{\partial t} + \mu S \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} \right) dt + \sigma S \frac{\partial V}{\partial S} dW_t
$$

### 4. 构造无风险投资组合

构造一个投资组合 $\Pi$，持有一个期权，卖出 $\Delta$ 股标的资产：
$$
\Pi = V - \Delta S
$$

其变化量：
$$
d\Pi = dV - \Delta dS
$$

代入 $dV$ 和 $dS$：
$$
d\Pi = \left( \frac{\partial V}{\partial t} + \mu S \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} \right) dt + \sigma S \frac{\partial V}{\partial S} dW_t - \Delta (\mu S dt + \sigma S dW_t)
$$

整理：
$$
d\Pi = \left( \frac{\partial V}{\partial t} + \mu S \frac{\partial V}{\partial S} - \Delta \mu S + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} \right) dt + \left( \sigma S \frac{\partial V}{\partial S} - \Delta \sigma S \right) dW_t
$$

选择：
$$
\Delta = \frac{\partial V}{\partial S}
$$

使得随机项消失：
$$
d\Pi = \left( \frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} \right) dt
$$

这是一个无风险的组合，因此其收益率应等于无风险利率 $r$：
$$
d\Pi = r \Pi dt = r (V - S \frac{\partial V}{\partial S}) dt
$$

### 5. 得到Black-Scholes偏微分方程（PDE）

将两边等式相等：
$$
\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} = r V - r S \frac{\partial V}{\partial S}
$$

整理得：
$$
\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} + r S \frac{\partial V}{\partial S} - r V = 0
$$

这就是著名的 **Black-Scholes偏微分方程**。

---

## 四、Black-Scholes公式的解析解

对于欧式看涨期权（Call option），行权价为 $K$，到期时间为 $T$，当前时间为 $t$，定义：
$$
\tau = T - t
$$

Black-Scholes公式给出期权价格为：
$$
C(S,t) = S N(d_1) - K e^{-r \tau} N(d_2)
$$

其中：
$$
d_1 = \frac{\ln \frac{S}{K} + \left(r + \frac{\sigma^2}{2}\right) \tau}{\sigma \sqrt{\tau}}, \quad d_2 = d_1 - \sigma \sqrt{\tau}
$$

$N(\cdot)$ 是标准正态分布的累积分布函数。

对应的欧式看跌期权（Put option）价格为：
$$
P(S,t) = K e^{-r \tau} N(-d_2) - S N(-d_1)
$$

# 希腊字母风险参数

进行期权交易的核心是需要理解其非线性收益特征，尤其是理解希腊字母相关风险参数(Delta, Gamma, Theta, Vega)