---
date: '2025-08-26T18:58:27+08:00'
draft: false
title: 'Cloudflare Workers用法'
categories:
  - tech
keywords:
  - cloudflare workers
  - next.js
tags:
  - cloudflare workers
  - next.js
---

# 概述

Cloudflare Workers是一个基于Cloudflare全球网络的serverless函数服务，它可以在 Cloudflare 的边缘网络上运行，为开发者提供了一种简单、灵活的方式来构建和部署应用程序。

## Hello, Cloudflare Workers

创建一个Worker项目: `pnpm create cloudflare@latest my-first-worker`，创建后项目中会包含以下几个比较关键的文件:

+ `wrangler.jsonc`: Wrangler配置问津
+ `index.js (in /src)`: 使用ES Module语法的Worker代码
+ `package.json`: 依赖配置

本地调试启动: `pnpm run dev`
worker部署: `pnpm run deploy`
