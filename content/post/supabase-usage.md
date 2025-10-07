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

# 身份认证Auth

## 一些基本概念

### session

Supabase auth提供对用户会话session的细粒度控制。当用户登录时会创建session, 默认情况下无限期延续，用户可以在任意数量的设备上拥有无限数量的action sessions.这些会话会存储在`auth.sessions`表中.

**会话以JWT形式的Supabase auth访问令牌和唯一的refresh token表示**，access token被设计为短期，通常在5min ~ 1h, 而refresh token不会过期，只能使用一次，而且只能通过交换一次refresh token来获取新的访问和refresh token对。这个过程称为**刷新会话refreshing the session**.

会话终止条件：用户注销、执行密码修改等安全敏感操作、长时间不活动、达到最大寿命、在另一台设备上登录。

每个access token都包含一个`session_id`声明即一个UUID， 用来唯一标识用户的会话，可以将这个ID与`auth.sessions`表的主键关联。

## JWT Web Token

JWT是具有如下结构的字符串：`<header>.<payload>.<signature>`, 每个部分都是Base64-URL编码的JSON或者字节。

header结构：

```json
{
  "typ": "JWT",
  "alg": "<HS256 | ES256 | RS256>",
  "kid": "<unique key identifier>"
}
```

header提供一些基本识别信息，如类型、加密算法、以及可选的验证时使用的标识符

payload结构：

```json
{
  "iss": "https://project_id.supabase.co/auth/v1",
  "exp": 12345678,
  "sub": "<user ID>",
  "role": "authenticated",
  "email": "someone@example.com",
  "phone": "+15552368"
  // ...
}
```

payload提供有关令牌表示的用户的标识信息（也叫声明claims），通常通常，JWT 会传达有关用户可以访问的内容（即对应acess token）或用户是谁（即对应ID token）的信息。声明信息有几个重要的字段：

1. iss: 表示颁发令牌的服务器
2. exp: 过期时间限制，超过时间也不应被信任
3. sub: 表示主题，是令牌表示的用户的唯一ID
4. role: 应用RLS(Row Level Security)策略时要使用的Postgres角色

> 需要添加、删除或者修改token中的声明信息，可以参见[Custom Access Token Hook](https://supabase.com/docs/guides/auth/auth-hooks/custom-access-token-hook)

signature使用对称或者非对称加密，用来验证`<header>.<payload>`字符串的真实性, 不依赖DB访问、身份验证服务器的活跃或者性能。

> 验证签名避免自己实现算法，而是依赖 `supabase.auth.getClaims()` 或其他高质量 JWT 验证库。

## JWT签名密钥管理最佳实践

只要用户保持登录状态，supabase auth会持续为每个用户会话发出新的JWT.

## getUser vs. getSession vs. getClaims

getSession返回会话信息，如果没有检测到session（如用户未登录或者注销）返回的会话可能是null。
> 这个方法是直接从客户端存储的值进行加载，如果存储基于请求cookie则其中的值可能是

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
