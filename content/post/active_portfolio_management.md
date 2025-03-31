---
date: '2025-03-20T10:45:47+08:00'
draft: false
title: '主动投资管理《Active Portfolio Management》阅读笔记'
categories:
  - quantitive
keywords:
  - Active Portfolio Management
tags:
  - Active Portfolio Management
description: ""
---

# 第一章

## 基础量化见解

Active Portfolio Management的七个量化见解：
1. consensus views lead to the benchmark.
2. The Information Ratio (IR) is the Key to Value-Added.
3. The Fundamental Law of Active Management:  IR = IC * sqrt(Breadth)
4. Alphas must control for volatility, skill, and expectations: Alpha = Volatility · IC · Score.
5. Why Datamining is Easy, and guidelines to avoid it.
6. Implementation should subtract as little value as possible.
7. Distinguishing skill from luck is difficult.

## 关注内容

我们的相对视角将聚焦于收益的剩余部分residual return:即与基准收益benchmark return无关的那部分收益。信息比率是预期年度剩余收益annual residual return与剩余收益年度波动率volatility之比。这一比率界定了主动型管理人可把握的投资机会空间 - 信息比率越大，主动管理的潜力就越大。

投资机会的选择取决于偏好。在主动管理中，偏好指向高剩余收益与低剩余风险。我们通过剩余收益减去对剩余风险的二次惩罚项(即对剩余方差的一次惩罚)，以均值-方差框架来刻画这一偏好。这可以理解为"风险调整后的预期收益risk-adjusted expected return"或"增值收益value-added"。我们可用无差异曲线 indifference curves来描述这种偏好关系 - 在获得相同增值收益的前提下，预期剩余收益与剩余风险的不同组合对我们而言是无差异的。每条无差异曲线都包含一个具有零剩余风险的"确定性等值"剩余收益。

## CAPM理论理解

CAPM 的一个有价值的副产品是确定共识预期收益consensus expected returns的程序。这些共识预期收益很有价值，因为它们为我们提供了比较标准。我们知道，我们的积极管理决策将取决于我们的预期收益与共识收益之间的差异。

1. The return of any stock can be separated into a systematic (market) component and a residual
component. No theory is required to do this. 任何股票的收益都可以分为系统（市场）部分和残差部分。这不需要任何理论
2. The CAPM says that the residual component of return has an expected value of zero. CAPM 表示收益的残差部分的预期值为零
3. The CAPM is easy to understand and relatively easy to implement.
4. There is a powerful logic of market efficiency behind the CAPM.
5. The CAPM thrusts the burden of proof onto the active manager. It suggests that passive
management is a lower-risk alternative to active management.
6. The CAPM provides a valuable source of consensus expectations. The active manager can
succeed to the extent that his or her forecasts are superior to the CAPM consensus forecasts.
7. The CAPM is about expected returns, not risk.