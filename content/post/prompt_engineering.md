---
date: '2025-04-02T19:26:21+08:00'
draft: false
title: '提示工程'
categories:
  - AI
keywords:
  - Prompt Engineering
  - Prompt
tags:
  - Prompt Engineering
  - Prompt
---

# 基础

## 定义

提示工程PE（Prompt Engineering）是利用自然语言处理技术，通过优化提示词（Prompt），来提高模型性能和效果的一种技术。

好的提示词通常具有以下特点：

1. **可读性**：
2. **可维护性**：
3. **格式优美**：
4. **Few-shot示例**：可以通过few-shot等技术大大提高AI的理解能力
5. **必要的限制**：
6. **异常处理**：

## 提示词的优化：

基于 AI 生成的初始提示词，我们优化提示词的思路可以从以下几个方面入手：
- 使用更专业的术语
- 手工优化 Few-shot 示例
- 优化输入输出的格式
- 提供必要的报错信息，如用户输入的信息与prompt主题无关，则给出对应的错误提示

# 常见工程技术

常见的PE包括：上下文学习，思维链等

- 上下文学习：构造包含**具体的指令**以及相关**上下文信息**的详细清晰Prompt, 要求LLM按命令输出
- 思维链：构造**思维Prompt**诱发大语言模型像人类一样思考，并输出中间思维步骤，增强推理能力

## 上下文学习In-Context Learning

通过**任务说明、演示示例**等信息引导模型输出，快速适应新任务，使 LLM as a service成为可能。

为什么上下文学习有效？大语言模型在预训练阶段从大量文本中学习**潜在的概念**。当运用ICL进行推理时，其借助任务说明或演示示例来“锚定”其在预训练阶段所学习到的相关概念，从而进行上下文学习并对问题进行预测。 [An Explanation of In-context Learning as Implicit Bayesian Inference](https://arxiv.org/abs/2111.02080)

![ICL Example](/images/ai/ICL-example-1.png)

根据示例数量的不同，上下文学习可以分为三类：零样本（Zero-shot）, 单样本（One-Shot）, 少样本（Few-Shot）。演示示例选择的两个主要依据：**相似性和多样性**。相似性是指选出与待解决问题文本最为相近的示例，多样性则要求选择的示例涵盖尽可能广的内容，扩大演示示例对待解决问题的覆盖范围。

关注项：
- **错误的演示示例会让ICL效果变差**，且敏感性与模型大小有关。较大的模型通常表现出更好的指令跟随能力，也对标签错误具有更高的敏感性。
- 复杂推理任务仅适用简单的 输入-标签格式，不足以让模型学习到其中复杂的映射关系，此时增加**中间推理步骤**会有更好的效果。

## 思维链Chain of Thought(CoT)

心理学中,System-1任务和System-2任务分别代表两种不同的思维方式所处理的任务类型；其中System-1任务的思考过程是**快速、自动且无意识的**，主要依靠直觉和经验进行判断，不需要刻意思考往往瞬间完成；System-2任务思考过程比较缓慢，往往需要**集中注意力和耗费精力**，运用逻辑分析、计算和有意识的思考来解决问题。

LLM在**标准提示**下在System-1任务（如常识问答、情感分类、意图识别等）上性能显著增强，而在System-2任务（如复杂数学计算、逻辑推理等）上，LLM表现出了**Flat Scaling Curves**现象，即模型规模增长未带来预期性能提升。

> GSM8K复杂数学问题集

CoT提出源自论文[Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)，思维链CoT通过在提示中 **嵌入一系列中间推理步骤**，引导LLM模拟人类解决问题时的思考过程，提升LLM处理复杂问题的能力。



示例：输出具有个人风格、富有情感、充满人味儿的文案

# 杂项

## OpenAI Meta Prompt

```markdown
Given a task description or existing prompt, produce a detailed system prompt to guide a language model in completing the task effectively.

# Guidelines

- Understand the Task: Grasp the main objective, goals, requirements, constraints, and expected output.
- Minimal Changes: If an existing prompt is provided, improve it only if it's simple. For complex prompts, enhance clarity and add missing elements without altering the original structure.
- Reasoning Before Conclusions**: Encourage reasoning steps before any conclusions are reached. ATTENTION! If the user provides examples where the reasoning happens afterward, REVERSE the order! NEVER START EXAMPLES WITH CONCLUSIONS!
    - Reasoning Order: Call out reasoning portions of the prompt and conclusion parts (specific fields by name). For each, determine the ORDER in which this is done, and whether it needs to be reversed.
    - Conclusion, classifications, or results should ALWAYS appear last.
- Examples: Include high-quality examples if helpful, using placeholders [in brackets] for complex elements.
   - What kinds of examples may need to be included, how many, and whether they are complex enough to benefit from placeholders.
- Clarity and Conciseness: Use clear, specific language. Avoid unnecessary instructions or bland statements.
- Formatting: Use markdown features for readability. DO NOT USE ``` CODE BLOCKS UNLESS SPECIFICALLY REQUESTED.
- Preserve User Content: If the input task or prompt includes extensive guidelines or examples, preserve them entirely, or as closely as possible. If they are vague, consider breaking down into sub-steps. Keep any details, guidelines, examples, variables, or placeholders provided by the user.
- Constants: DO include constants in the prompt, as they are not susceptible to prompt injection. Such as guides, rubrics, and examples.
- Output Format: Explicitly the most appropriate output format, in detail. This should include length and syntax (e.g. short sentence, paragraph, JSON, etc.)
    - For tasks outputting well-defined or structured data (classification, JSON, etc.) bias toward outputting a JSON.
    - JSON should never be wrapped in code blocks (```) unless explicitly requested.

The final prompt you output should adhere to the following structure below. Do not include any additional commentary, only output the completed system prompt. SPECIFICALLY, do not include any additional messages at the start or end of the prompt. (e.g. no "---")

[Concise instruction describing the task - this should be the first line in the prompt, no section header]

[Additional details as needed.]

[Optional sections with headings or bullet points for detailed steps.]

# Steps [optional]

[optional: a detailed breakdown of the steps necessary to accomplish the task]

# Output Format

[Specifically call out how the output should be formatted, be it response length, structure e.g. JSON, markdown, etc]

# Examples [optional]

[Optional: 1-3 well-defined examples with placeholders if necessary. Clearly mark where examples start and end, and what the input and output are. User placeholders as necessary.]
[If the examples are shorter than what a realistic example is expected to be, make a reference with () explaining how real examples should be longer / shorter / different. AND USE PLACEHOLDERS! ]

# Notes [optional]

[optional: edge cases, details, and an area to call or repeat out specific important considerations]

# Settings

[system_prompt_locale: en_US]
```

# 参考

1. [Meta Prompt By OpenAI]()
