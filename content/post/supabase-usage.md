---
date: '2025-10-03T02:56:00+08:00'
draft: false
title: 'Supabase使用'
categories:
  - tech
keywords:
  - supabase
  - postgres
  - auth
tags:
  - supabase
  - postgres
  - auth
---

# 概述

Supabase 是一个开源的 Firebase 替代品，它提供了一系列后端即服务功能。**supabase = PostgreSQL 数据库 + 一系列内置工具**

1. Supabase 的核心是一个全托管的 PostgreSQL 数据库；可以基于你的数据库结构，它会自动、实时地生成 REST 和 GraphQL API。
2. 身份认证Authentication:  内置了完整的用户管理系统，支持邮箱/密码、魔法链接、第三方 OAuth (Google, GitHub, Apple 等)
3. 存储Storage: 用于管理用户上传的文件（如图片、视频、文档等）

# MCP

# 身份认证

## OAuth申请

### Google OAuth申请

### Github OAuth申请

申请地址 [github developer settings](https://github.com/settings/developers), 回调地址参考下方进行配置。

默认的回调地址URL应该是类似：`[origin]/api/auth/callback/[provider]`的格式，例如：

```javascript
// Local
http://localhost:3000/api/auth/callback/github
 
// Prod
https://app.company.com/api/auth/callback/github
```
