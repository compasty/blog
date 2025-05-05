---
date: '2025-03-19T20:17:16+08:00'
draft: false
title: '机器学习数学基础'
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

# 概率论&统计

## Z-score标准分数

在统计学中，Z-score（标准分数）是一种用于衡量数据点与均值之间距离的标准化方法。它表示数据点与均值之间的距离，以标准差为单位。Z-score 可以帮助我们理解数据点在分布中的相对位置，并且在**比较不同数据集，识别异常值（z-score较大的值）**时非常有用。

Z-score 的公式如下：$Z= \frac{X - \mu}{\sigma}$, 其中: $\mu$表示均值，$\sigma$表示数据集的标准差。

可以使用 `scipy.stats.zscore` 进行计算。

## L1/L2正则化


