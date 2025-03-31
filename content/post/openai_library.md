---
date: '2025-03-23T19:21:48+08:00'
draft: false
title: 'OpenAI库使用'
categories:
  - AI
keywords:
  - OpenAI
tags:
  - OpenAI
---

# 基础

OpenAI Python库是OpenAI官方提供的开发工具包，旨在帮助开发者快速集成GPT系列模型、DALL·E图像生成等AI能力。截至2025年3月，该库已迭代至v2.x版本，支持同步/异步调用、流式响应等特性，并新增了Agent开发工具链。

## 核心概念 

### 补全Completion

Completions是API的核心，提供了一个非常灵活和强大的简单接口。您将一些文本作为**提示(Prompt)输入**，API将返回一个**文本补全(Completion)**，试图匹配您给它的任何指令或上下文。

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key="${xxxx}",
    base_url="${xxx}",
)
prompt = "为一家咖啡店写一个店名和标语"
completion = client.chat.completions.create(
    model="gpt-4o",
    temperature=0.2,
    messages=[
        {'role': 'system', 'content': 'You are a helpful assistant.'},
        {'role': 'user', 'content': prompt}
        ]
)
print(completion.choices[0].message.content)
```

### temperature

**Temperature（温度参数）**是控制语言模型生成文本**随机性**的核心参数，通过调节输出概率分布的平滑程度，直接影响生成内容的创造性和确定性。

温度参数底层通过softmax函数调节token概率分布: $P'(wi) = exp(logP(wi)/T) / Σ(exp(logP(wj)/T))$

其中:

- **T=1**：保持原始概率分布
- **T→0**：趋向贪心搜索（选择最高概率token）
- **T>1**：平滑概率分布，增强低概率token的竞争力

所以，一般需要高确定性输出的场景：如技术文档生成、代码补全等建议设置较小的temperature, 如0 ~ 0.2，而对于需要高度随机性/创造性的场景如诗歌创作、营销创作则建议设置相对较高的temperature，如0.8 ~ 1.0，商业文案、客服对话等需要兼顾创造性和逻辑性的场景建议设置为0.3 ~ 0.6。

### 标记tokens

**Tokens（标记）**是语言模型处理文本的基本单元，相当于自然语言处理的"原子单位"。通过将文本分割为tokens序列，模型能够：
- 理解词语的上下文含义
- 建立词与词之间的关联模式
- 生成符合语言逻辑的文本

常见的分割形式：

| 语言类型 | 典型分割方式                   | 示例                       |
|----------|------------------------------|---------------------------|
| 英语     | 单词/子词分割                 | "unbelievable" → ["un", "belie", "vable"] |
| 中文     | 单字/常用词组合               | "人工智能" → ["人", "工", "智能"] |
| 代码     | 保留关键字与符号              | "print('hello')" → ["print", "(", "'hello'", ")"] |

可以使用`tiktoken`来查看具体token拆分的效果:

```python
from tiktoken import get_encoding
encoder = get_encoding("cl100k_base")
print(encoder.encode("自然语言处理"))
```

一些最佳实践:

1. 设置`max_tokens`防止意外消耗, 或使用`tiktoken`进行token量级预估
2. 对于超长文本使用分块处理
3. 明确提示词降低冗余输出



# 参考

1. [openai-python](https://github.com/openai/openai-python)
2. [OpenAI中文开发文档](https://www.openaidoc.com.cn/docs/quickstart)

