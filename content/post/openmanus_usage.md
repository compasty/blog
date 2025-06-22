---
date: '2025-04-01T21:36:31+08:00'
draft: false
title: 'OpenManus学习记录'
categories:
  - AI
keywords:
  - manus
  - OpenManus
tags:
  - manus
  - OpenManus
---

# 基础

[OpenManus](https://github.com/mannaandpoem/OpenManus)是Manus的一套开源实现。

## Hello, Manus

1. 模型配置, 在目录config下面复制`config.example.toml`改名为`config.toml`, 然后更新模型配置信息。以使用qwen模型为例:

```toml
# Global LLM configuration
[llm]
model = "qwq-plus"        # The LLM model to use
base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"  # API endpoint URL
api_key = "sk-xxxxx"                    # Your API key
max_tokens = 8192                           # Maximum number of tokens in the response
temperature = 0.0                           # Controls randomness

# Optional configuration for specific LLM models
[llm.vision]
model = "qwen-vl-max"        # The vision model to use
base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"  # API endpoint URL for vision model
api_key = "sk-xxxx"                    # Your API key for vision model
max_tokens = 8192                           # Maximum number of tokens in the response
temperature = 0.0                           # Controls randomness for vision model
```

# 结合MCP

## OpenManus MCP 架构设计

### MCP 主机及客户端（MCPAgent）
OpenManus 中 MCP 主机及客户端相关的实现位于`app/agent/mcp_agent.py`和`app/tool/mcp.py`
- 通过 stdio 或 SSE 等方式连接到 MCP 服务器
- 动态发现可用工具
- 通过向服务器传递请求来执行工具
- 处理工具响应和错误

### MCP 服务器
OpenManus 提供的 MCP 服务器位于`app/server.py`
- 使用 FastMCP 注册工具
- 通过标准化接口提供工具
- 处理工具执行、参数验证和结果格式化

MCP服务器提供了以下OpenManus核心工具的访问:
1. **BrowerUse**: 网页操作
2. **Bash**: 执行命令，处理命令输出和错误等
3. **StringReplaceEditor**: 查看、创建和编辑文件，提供精确的字符串替换功能
4. **Terminate**: 控制程序执行流程，优雅结束交互会话

# 使用经验

1. 在一些趣味性和需要创造力的想法中，temperature调到0.7可以增加随机性
2. 生成结果比较离谱的时候可以考虑下面的prompt: **用小学生能听懂的话解释**

# 参考

1. [OpenManus 新手保姆教程 - 初级入门](https://404digital.feishu.cn/docx/TO6WdA64OoDsevxo4Zpc7HuCn4g)