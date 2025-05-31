---
date: '2025-04-21T18:59:53+08:00'
draft: false
title: 'Worldquant操作符详解'
categories:
  - quantitive
keywords:
  - quant alpha
  - worldquant brain
tags:
  - quant alpha
  - worldquant brain
mathjax: true
---

# 基础

## 横截面操作符 vs. 时序操作符

让我们想象一个学生在一次考试中得了80分。有两种主要的方法来评估这个分数：与自己过去的成绩进行比较，或者与其他学生在这次考试中的成绩进行比较。和自己的历史比，这类操作一般称为时间序列操作符(Time Series operators)；和其他学生比，这类操作一般称为横截面操作符 Cross-Sectional Operators）。

![sample](/images/quantitive/brain_sample_data.png)

以上图为例，红色标记区域表示用于时间序列计算的数据，绿色标记区域表示用于横截面计算的数据。

代表性的时间序列操作符：`ts_mean`, `ts_zscore`, `ts_rank`. 代表性的横截面操作符：`rank`, `zscore`, `winsorize`.

# 常用操作符详解

## trade_when

`trade_when`操作符常用来进行条件化交易，可以决定何时更新值。语法格式为：`trade_when (x=triggerTradeExp, y=AlphaExp, z=triggerExitExp)`, 三个入参分别表示：入场条件、Alpha 表达式和出场条件。

在计算时，首先会计算triggerExitExp，如果triggerExitExp>0, 则Alpha=NaN, 然后如果triggerTradeExp>0, 则Alpha按照AlphaExp更新值, 否则Alpha保持入场条件为真时的最后一个阿尔法值。

例如：`trade_when(volume >= ts_mean(volume,5), rank(-returns), abs(returns) > 0.1)`, 如果回报绝对值大于0.1则退出，否则当成交量大于5日成交量均值时，alpha更新为`rank(-returns)`, 否则alpha仍保持前值。

## ts_backfill

`ts_backfill(x, lookback = d, k = 1, ignore = "NAN")`

`ts_backfill`操作符会用最后一个可用的非 NaN 值替换 NaN 值。如果数据字段 x 的输入值为 NaN，ts_backfill 操作符将检查过去 d 天内相同数据字段的可用输入值，并输出最近的可用非 NaN 输入值。如果设置了 k 参数，那么 ts_backfill 操作符将输出第 k 个最近的可用非 NaN 输入值。

该操作提高了权重覆盖率，可能有助于降低回撤风险。例如`ts_backfill(x, 252)`表示若字段x的输入值为NaN，则用最近252天内x的非NaN值替换, 可用于年更新级别的数据字段回填。

## winsorize

winsorize通过截断数据中的极端值，将其限制在`[均值 - std × 标准差, 均值 + std × 标准差]`范围内，再基于截断后的数据计算统计量（如均值）。

运行步骤：首先剔除数据中的NaN值，计算剩余数据的均值（`μ`）和标准差（`σ`）, 然后根据`std`参数的值计算上下限，最后将超出边界的值替换边界值（即小于下限的值改为下限值，大于上限的改为上限值），返回处理后的数据。

与截尾（Trimming）的区别是：Winsorizing 不会删除数据，而是将极端值替换为边界值，而 Trimming 会删除极端值。

## bucket

bucket常用于自定义分组