---
date: '2025-09-02T17:13:09+08:00'
draft: false
title: 'Embedding Models从架构到实现'
categories:
  - AI
keywords:
  - embedding models
  - transformers
  - bert
tags:
  - embedding models
  - transformers
  - bert
---

# 概述

随着人工智能和自然语言处理（NLP）的快速发展，Embedding Model（嵌入模型）已成为理解和处理文本、图像、音频等数据的核心技术之一。

## 什么是Embedding Model?

Embedding Model是一类将离散对象（如单词、句子、图像等）映射为连续向量空间的方法。通过这种方式，模型能够捕捉对象之间的语义或结构关系，便于后续的机器学习任务处理。

## 发展阶段

1. One-hot Encoding（独热编码）

最早期的表示方法是One-hot编码。每个词用一个高维稀疏向量表示，只有一个维度为1，其余为0。这种方法简单直观，但无法表达词与词之间的语义关系，且维度随词表大小线性增长，效率低下。

2. 基于计数的分布式表示（如LSA）

为了解决One-hot的不足，出现了基于统计的分布式表示方法。例如，**LSA（Latent Semantic Analysis）**通过SVD等矩阵分解技术，从词-文档共现矩阵中提取低维语义空间。虽然一定程度上捕捉了词语之间的关系，但计算复杂度高，扩展性有限。

3. 神经网络词向量（Word Embedding）

在2013年前后，随着神经网络的发展，出现了革命性的词向量模型：
  - Word2Vec（2013）

    由Google提出，包括CBOW和Skip-gram两种结构。通过预测上下文或中心词，学习到低维稠密的词向量，能够很好地捕捉词语的语义和句法关系。
  - GloVe（2014）

    由斯坦福提出，结合了全局统计信息和局部上下文，进一步提升了词向量的表达能力。

这些模型的出现，使得“king - man + woman ≈ queen”这样的语义运算成为可能。

4. 上下文相关的Embedding（Contextualized Embedding）

传统的Word Embedding为每个词分配唯一向量，无法处理多义词。为此，出现了上下文相关的嵌入模型：
  - ELMo（2018）

    基于双向LSTM，能够根据上下文动态生成词向量。
  - BERT（2018）及其变体

    采用Transformer结构，利用双向编码，极大提升了语义理解能力。BERT不仅为词生成上下文相关的向量，还能为句子、段落生成嵌入。

5. 多模态与跨领域Embedding

随着需求的提升，Embedding模型也扩展到图像、音频等领域，甚至实现了多模态融合：
  - CLIP（2021）

    由OpenAI提出，将图像和文本映射到同一向量空间，实现了跨模态检索和理解。
  - Sentence Embedding、Document Embedding
  
    如Sentence-BERT等模型，专门针对句子、文档级别的表示，提升了下游任务的效果。



# 参考

1. [Embedding Models: from Architecture to Implementation](https://learn.deeplearning.ai/courses/embedding-models-from-architecture-to-implementation/lesson/vu3si/introduction)
