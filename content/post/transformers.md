---
date: '2025-03-18T20:51:32+08:00'
draft: false
title: 'Transformers学习记录'
categories:
  - AI
tags:
  - transformers
keywords:
  - transformers
description: 'Transformers理论学习与使用实践'
---

# NLP基础

自然语言处理（Natural Language Processing，NLP）是一门借助计算机技术研究人类语言的科学。


## NLP发展史

1. 1970年代以前: 基于文法规则，问题：自然语言是上下文有关文法，规则无法穷举
2. 1970年代 ~ 2006年: 基于数学模型和统计方法的自然语言处理方法开始兴起, 如“通信系统加隐马尔可夫模型”，有向图
3. 2006年 ~ 2017年: 辛顿（Hinton）证明深度信念网络（Deep Belief Networks，DBN）可以通过逐层预训练策略有效地进行训练, 深度学习方法兴起(CNN, LSTM)
4: 2017年 ~ 至今: Google 公司提出了 Attention 注意力模型，Transformer结构几乎一统江湖

# 参考

1. [Transformers快速入门]https://transformers.run/