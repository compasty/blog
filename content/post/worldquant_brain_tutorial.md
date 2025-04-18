---
date: '2025-04-02T14:56:52+08:00'
draft: false
title: 'Worldquant Brain学习记录'
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

## 什么是BRAIN平台？

利用定量分析方法，BRAIN平台是一个全球金融市场回测模拟器，接受Alpha表达式作为输入，并绘制其盈亏（PnL）作为输出.每天根据历史日期对每个金融工具的输入表达进行评估，并据此构建投资组合。BRAIN平台根据表达式的值对每种金融工具进行投资。它进行交易（买入或卖空），并为每种工具分配权重。

## 什么是Alpha?

对于 WorldQuant 来说， Alpha 是一个数学模型，旨在预测各种金融工具的未来价格走势 。它将输入数据（价格-成交量、新闻、基本面等）转化为一个向量，其中的数值与我们每天要持有的每种金融工具的头寸和权重成正比。

### BRAIN如何进行alpha回测

[参考](https://platform.worldquantbrain.com/learn/documentation/create-alphas/how-brain-platform-works)

假设回测的表达是`rank(-returns)`,并使用市场中性化、延迟1和衰减0设置, 则整个工具类似下图 （假设股票池中有8个股票）:

![brain_alpha](/images/quantitive/brain_works.png)

具体来讲:
1. **alpha求值**: 根据表达式生成给定日期的alpha向量，对应上面的D列
2. **中性化**：从向量中的每个值中减去该组向量值的平均值。使得所有向量值的总和=0，对应上面的F列。
3. **权重标准化**：将生成的值缩放或"标准化"，使得alpha向量值的绝对值总和为1。通常做法：原始值除以绝对值加和, 对应上面的H列。
4. **分配资金**：将资金根据3中得到的归一化权重分配资金，正值做多负值做空，NAN表示不分配资金。这被称为*多空市场中性化*，这是创建这些预测模型或alpha的支柱。使用这种技术，策略可以在市场走势方向不确定的情况下实现盈利.
5. **收益计算**: 根据当天观察到的股票回报率计算alpha生成的下一天的收益，例如K列表示实际回报率，则最终收益结果为L列。
6. **回测周期**: 对历史时间跨度IS中每个日期重复计算，得到累积PnL图表

> 1. 在BRAIN平台上，我们对回测的每一天**都使用恒定的账面大小**，无论你的投资组合是赚钱还是亏钱。
> 2. 如果使用行业中心化，则回测器会根据行业分组的情况对每个组执行相同的操作，最后将每个组的PnL相加以获得alpha的每日PnL，并创建累积PnL图表。

### 什么是好的Alpha？

一个好的阿尔法最好是有持续增长的净值，高的年回报率，更重要的是，在累积利润图中的波动很小。如果标准差较低，图表中的波动就会较小。如果图表中显示出高波动/波幅，尽管回报率很高，那么阿尔法就不会被认为是足够好。

WorldQuant旨在开发具有低波动性和低风险的股票多空市场中性阿尔法指数。其目标是最大限度地减少市场风险，并从两只股票的价差变化中获利。

## 模拟设置参数说明

1. Neutraliz

## 一些概念

1. PnL: Profit and Loss, 损益，在brain平台一般表示累计盈亏
2. IS: Inside Sample, 在brain平台表示样本内期间
3. OS: Outside Sample, 在brain平台表示样本外期间
4. Sharpe Ratio: 该比率衡量Alpha策略的超额回报（或风险溢价）与其波动性之间的比率。它将PnL的平均值除以PnL的标准差, 公式为:$Sharpe Ratio=$。Sharpe Ratio或信息比率（IR）越高，Alpha策略潜在的回报越稳定，而稳定性是一个理想的特征。BRAIN平台的Sharpe Ratio通过要求为大于1.25来判断是否通过.
5. IC: Information Coefficient是衡量量化因子预测能力的一种指标。通常使用 Spearman 秩相关系数或 Pearson 相关系数来计算。一个较高的 IC 表示因子对未来收益有较好的预测能力。
    - Spearman 秩相关系数：用于衡量因子值与实际收益之间的秩相关性，适用于非线性关系。
    - Pearson 相关系数：用于衡量因子值与实际收益之间的线性相关性，适用于线性关系。

```python
import numpy as np
from scipy.stats import spearmanr
# 示例数据
factor_values = np.array([0.1, 0.4, 0.3, 0.5, 0.2])
actual_returns = np.array([0.05, 0.12, 0.08, 0.15, 0.07])
# 计算 Spearman 秩相关系数
spearman_ic, _ = spearmanr(factor_values, actual_returns)
print("Spearman IC:", spearman_ic)
# 计算 Pearson 相关系数
pearson_ic = np.corrcoef(factor_values, actual_returns)[0, 1]
print("Pearson IC:", pearson_ic)
```

# Fast Expression语法

## 基础



## 运算符Operators

# WorldQuant Brain 运算符表格指南

## 基础运算符

| 运算符名称       | 语法                                | 描述                                                                                     | 参数说明                     |
|------------------|-------------------------------------|------------------------------------------------------------------------------------------|------------------------------|
| **绝对值**       | `abs(x)`                           | 返回 x 的绝对值                                                                          | -                            |
| **加法**         | `add(x, y, filter=false)` 或 `x + y` | 对输入值求和（至少需 2 个输入）                                                          | `filter=true` 将 NaN 替换为 0 |
| **除法**         | `divide(x, y)` 或 `x / y`           | 返回 x 除以 y 的结果                                                                     | -                            |
| **倒数**         | `inverse(x)`                        | 返回 1 / x                                                                               | -                            |
| **自然对数**     | `log(x)`                            | 返回 x 的自然对数（例如 `Log(high/low)` 计算价格比值的对数）                             | -                            |
| **最大值**       | `max(x, y, ...)`                    | 返回所有输入中的最大值（至少需 2 个输入）                                                | -                            |
| **最小值**       | `min(x, y, ...)`                    | 返回所有输入中的最小值（至少需 2 个输入）                                                | -                            |
| **乘法**         | `multiply(x, y, ..., filter=false)` 或 `x * y` | 对输入值求积（至少需 2 个输入）                                                           | `filter=true` 将 NaN 替换为 1 |
| **幂运算**       | `power(x, y)`                       | 返回 x 的 y 次幂                                                                         | -                            |
| **反向值**       | `reverse(x)`                        | 返回 -x                                                                                  | -                            |
| **符号函数**     | `sign(x)`                           | 若输入为 `NaN` 返回 `NaN`；否则返回 x 的符号（-1, 0, 1）                                  | -                            |
| **带符号的幂**   | `signed_power(x, y)`                | 返回 x 的 y 次幂，并保留 x 的符号                                                        | -                            |
| **平方根**       | `sqrt(x)`                           | 返回 x 的平方根                                                                          | -                            |
| **减法**         | `subtract(x, y, filter=false)` 或 `x - y` | 返回 x 减 y                                                                               | `filter=true` 将 NaN 替换为 0 |
| **稀疏化**       | `densify(x)`                        | 将分组字段的多个桶合并为更少的可用桶以提高计算效率                                        | -                            |

---

## 逻辑运算符

| 运算符名称       | 语法                  | 描述                                                                 | 参数说明 |
|------------------|-----------------------|----------------------------------------------------------------------|----------|
| **逻辑与**       | `and(input1, input2)` | 仅当两个输入均为真时返回 `true`                                      | -        |
| **逻辑或**       | `or(input1, input2)`  | 任一输入为真时返回 `true`                                            | -        |
| **逻辑非**       | `not(x)`              | 输入为真返回 `false`，输入为假返回 `true`                            | -        |
| **小于**         | `input1 < input2`     | 若 `input1 < input2` 返回 `true`                                     | -        |
| **小于等于**     | `input1 <= input2`    | 若 `input1 <= input2` 返回 `true`                                    | -        |
| **等于**         | `input1 == input2`    | 若两个输入相等返回 `true`                                            | -        |
| **大于**         | `input1 > input2`     | 若 `input1 > input2` 返回 `true`                                     | -        |
| **大于等于**     | `input1 >= input2`    | 若 `input1 >= input2` 返回 `true`                                    | -        |
| **不等于**       | `input1 != input2`    | 若两个输入不相等返回 `true`                                          | -        |
| **是否为 NaN**   | `is_nan(input)`       | 若输入为 `NaN` 返回 1，否则返回 0                                    | -        |
| **条件选择**     | `if_else(input1, input2, input3)` | 若 `input1` 为真返回 `input2`，否则返回 `input3`                      | -        |

---

## 时间序列运算符

| 运算符名称          | 语法                                  | 描述                                                                                     | 参数说明                     |
|---------------------|---------------------------------------|------------------------------------------------------------------------------------------|------------------------------|
| **移动平均值**      | `ts_mean(x, d)`                      | 返回过去 d 天内 x 的平均值                                                               | -                            |
| **滚动求和**        | `ts_sum(x, d)`                       | 返回过去 d 天内 x 的累加值                                                               | -                            |
| **延迟值**          | `ts_delay(x, d)`                     | 返回 d 天前的 x 值                                                                       | -                            |
| **差值计算**        | `ts_delta(x, d)`                     | 返回当前 x 值减去 d 天前的 x 值（即 `x - ts_delay(x, d)`）                               | -                            |
| **Z 分数**          | `ts_zscore(x, d)`                    | 计算标准化分数：(x - ts_mean(x,d)) / ts_std_dev(x,d)，用于减少异常值                     | -                            |
| **最大值索引**      | `ts_arg_max(x, d)`                   | 返回过去 d 天内最大值对应的相对天数索引（当前天为 0）                                    | -                            |
| **最小值索引**      | `ts_arg_min(x, d)`                   | 返回过去 d 天内最小值对应的相对天数索引（当前天为 0）                                    | -                            |
| **数据回填**        | `ts_backfill(x, lookback=d, k=1)`    | 用过去 d 天内第 k 个非 `NaN` 值填充当前 `NaN`                                            | `ignore="NAN"` 控制填充规则  |
| **相关系数**        | `ts_corr(x, y, d)`                   | 返回 x 和 y 在过去 d 天内的相关系数                                                      | -                            |
| **滚动排名**        | `ts_rank(x, d, constant=0)`          | 对过去 d 天内的 x 值排序，返回当前值的排名 + `constant`                                  | `constant` 为排名偏移量      |

---

## 横截面运算符

| 运算符名称        | 语法                                | 描述                                                                                     | 参数说明                     |
|-------------------|-------------------------------------|------------------------------------------------------------------------------------------|------------------------------|
| **标准化**        | `normalize(x, useStd=false)`       | 减去均值（若 `useStd=true` 则除以标准差）                                               | `limit` 限制标准化范围       |
| **排名**          | `rank(x, rate=2)`                  | 返回 0.0~1.0 的均匀分布排名（`rate=0` 表示精确排序）                                    | `rate` 控制排名精度          |
| **缩放**          | `scale(x, scale=1)`                | 将输入缩放到指定规模，可分别设置多头和空头比例（`longscale`, `shortscale`）             | -                            |
| **截尾处理**      | `winsorize(x, std=4)`              | 将 x 限制在均值的 ±`std` 倍标准差范围内                                                 | -                            |
| **横截面 Z 分数** | `zscore(x)`                        | 计算横截面 Z 分数：(x - 均值) / 标准差                                                  | -                            |

---

## 分组运算符

| 运算符名称          | 语法                      | 描述                                                                                     | 参数说明                     |
|---------------------|---------------------------|------------------------------------------------------------------------------------------|------------------------------|
| **组中性化**        | `group_neutralize(x, group)` | 消除组内（如行业、国家）的影响，使 Alpha 在组内中性化                                   | `group` 指定分组字段         |
| **组 Z 分数**       | `group_zscore(x, group)`  | 计算组内 Z 分数：(x - 组均值) / 组标准差                                                | -                            |
| **组内排名**        | `group_rank(x, group)`    | 在组内对每个元素分配排名                                                                | -                            |
| **组内归一化**      | `group_scale(x, group)`   | 将组内值缩放到 0~1 范围：(x - 组最小值) / (组最大值 - 组最小值)                         | -                            |

---

## 其他运算符

| 类别          | 运算符名称          | 语法                                | 描述                                                                                     |
|---------------|---------------------|-------------------------------------|------------------------------------------------------------------------------------------|
| **向量运算**  | 向量均值            | `vec_avg(x)`                       | 返回向量字段 x 的均值                                                                   |
|               | 向量求和            | `vec_sum(x)`                       | 返回向量字段 x 的总和                                                                   |
| **转换运算**  | 分桶                | `bucket(rank(x), range="0,1,0.1")` | 将浮点值转换为自定义区间的索引（用于分组）                                               |
|               | 条件交易            | `trade_when(x, y, z)`              | 仅在满足条件时更新 Alpha 值（如 `y` 触发时使用 `z` 逻辑）                                |



# 结果评估

## 结果报告

在BRAIN平台中，执行完模拟后会输出累计PnL图表，IS（样本内测试）概要。




IS（样本内测试）回测使用5年时间范围内的数据，测试您的Alpha策略在历史时期的表现如何。模拟后，您将看到IS概要行，其中包括6个指标：Sharpe、Turnover、Fitness、Returns、Drawdown和Margin。


