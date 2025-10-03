---
date: '2025-10-02T14:04:34+08:00'
draft: false
title: 'KouriChat项目agent设计分析'
categories:
  - AI
keywords:
  - KouriChat
  - Agent Design
tags:
  - KouriChat
  - Agent Design
---

# 概述

[KouriChat](https://github.com/KouriChat/KouriChat)是一个虚拟角色聊天软件，微信无缝接入（支持群聊），支持：

- 智能对话分段 & 情感化表情包
- 图像生成 & 图片识别（Kimi集成）
- 语音消息 & 持久记忆存储

# 代码结构解析

核心入口是`src/main.py`, 其中包含了处理私聊和处理群聊的机器人，这里只分析处理私聊的机器人, 对应类是`PrivateChatBot`.这其中分别初始化

## 配置项

`KouriChat`的配置包含以下几个部分，对应`data/config/__init__.py`

1. `user: UserSettings`: 用户设置，对应监听的用户列表和群聊列表
2. `llm: LLMSettngs`: 大模型设置，如`api_key`， `base_url`, `max_tokens`（回复最大token数量）等
3. `media: MediaSettings`: 多媒体模型设置，包含图像识别模型配置，图像生成模型配置，TTS模型设置等
4. `behavior: BehaviorSettings`: 行为设置，包含自动消息设置（定时发送的消息），context设置（包含最大上下文轮数、人设目录）
5. `auth: AuthSettings`: 授权设置
6. `network_search: NetworkSearchSettings`: 网页搜索和内容抓取模型设置
7. `intent_recognition: IntentRecognitionSettings`: 意图识别模型设置

人设目录包含`avatar.md`和`emojis`目录，其中`avatar.md`会作为prompt内容，emojis目录会按照情感类型划分目录（支持的情感类型实现参见: `src/handlers/emoji.py`）

## 代码入口

`KouriChat`是基于[wxauto](https://github.com/cluic/wxauto)实现的微信自动化，`wxauto`会暴露一个`AddListenChat`方法实现对于指定用户的微信消息监听.

## 记忆处理

角色+用户对应一套记忆
