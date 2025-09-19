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

+ `wrangler.jsonc`: Wrangler配置文件（Wrangler是Cloudflare提供的一个命令行工具，用于部署和管理Cloudflare Workers）
+ `index.js (in /src)`: 使用ES Module语法的Worker代码
+ `package.json`: 依赖配置

本地调试启动: `pnpm run dev`
worker部署: `pnpm run deploy`


默认的`index.js`文件内容如下:
```javascript
export default {
  async fetch(request, env, ctx) {
    return new Response("Hello World!");
  },
};
```

当worker接收http请求时，会调用`fetch`方法，也可以别的event handlers来处理不同类型的请求，例如: `scheduled()`方法处理从 `Cron Trigger` 触发的请求。
`fetch`方法返回`Response`对象或者一个`Promise`对象(resolve后返回`Response`对象)。

## Workers详细使用

### 环境变量

环境变量可以在`fetch`函数的`env`变量中进行获取，环境变量使用`.wrangler.json`的`vars`字段，如果需要区分不同的环境使用不同的变量则可以使用`env`字段，在命令行使用的时候可以用`--env`或者`-e`标志来进行环境的指定，例如：`pnpm dlx wrangler dev -e staging`

```json
{
  "name": "my-worker-dev",
  "vars": {
    "API_HOST": "example.com",
    "API_ACCOUNT_ID": "example_user",
    "SERVICE_X_DATA": {
      "URL": "service-x-api.dev.example",
      "MY_ID": 123
    }
  },
  "env": {
    "staging": {
      "vars": {
        "API_HOST": "staging.example.com"
      }
    },
    "production": {
      "vars": {
        "API_HOST": "production.example.com"
      }
    }
  }
}
```

> 永远不要将敏感信息存储在环境变量中，而是使用secret进行管理

### secret

secret是一种特殊的绑定类型，允许将加密文本值附加到workers。密钥在传递给worker的`fetch`方法中的`env`参数中可以被访问，可以通过支持Node.js兼容性的workers中`process.env`访问。

```javascript
const sql = postgres(env.DB_CONNECTION_STRING);

const result = await sql`SELECT * FROM products;`;
```

添加secret: `pnpm dlx wrangler secret put <KEY>`, 或者通过Cloudflare的配置页面进行添加
删除secret: `pnpm dlx wrangler secret delete <KEY>`

本地开发时一般将敏感信息存储在`.dev.vars`文件中或者`.env`文件中。

> `.dev.vars` 和 `.env` 文件不应提交到 git。将 `.dev.vars*` 和 `.env*` 添加到项目的 `.gitignore` 文件中


## 配套产品

### Hyperdrive

Hyperdrive 可以加速Cloudflare Workers 对现有数据库的访问，即使是单区域数据库也能感觉遍布全球。通过在 Cloudflare 网络中维护与数据库的连接池，Hyperdrive 在您发送查询之前减少了对数据库的七次往返：TCP 握手 （1x）、TLS 协商 （3x） 和数据库身份验证 （3x）。

> Hyperdrive 通过管理与源数据库的全局连接数量、有选择地解析和选择要缓存的查询响应，以实现减少数据库负载并加速数据库查询。

Hyperdrive的实现原理：
1. 为workers附近新数据连接执行连接设置
2. 池化离数据库地域较近的现有连接
3. 缓存查询结果

