---
date: '2025-06-19T13:26:06+08:00'
draft: false
title: 'Nextjs框架使用学习'
categories:
  - tech
keywords:
  - nextjs
  - vercel
tags:
  - nextjs
  - vercel
---

## 0. 引言

[Next.js](https://nextjs.org/docs) 是一个基于 React 的服务端渲染（SSR）框架，它不仅支持静态生成（SSG），还内置了强大的路由系统，极大简化了 React 应用的开发流程。

## 1. 入门

### 1.1 项目创建

创建Next.js应用最简单的方法就是使用`create-next-app`（要求nodejs 18.18+）: `npx create-next-app@latest`。

> 使用`pnpm`可以使用命令: `pnpm dlx create-next-app@latest`

### 1.2 路由模式(Router)

Next.js包含两种路由模式，`App Router`和`Page Router`，对应不同的目录结构和特性。


| 特性           | Page Router                      | App Router                      |
|----------------|--------------------------------|--------------------------------|
| 目录位置       | `pages/` 目录                  | `app/` 目录                   |
| 路由定义       | 通过文件和文件夹自动映射路由    | 通过文件夹和 `page.tsx` 组件定义路由 |
| 数据获取         | `getStaticProps`, `getServerSideProps`, `getStaticPaths` | 直接在组件中使用 `async` 函数（如 `fetch`）支持服务器组件 |
| 服务器组件支持   | 不支持                           | 原生支持服务器组件（Server Components） |
| 嵌套路由           | 通过嵌套文件夹实现             | 通过嵌套文件夹和布局（`layout.tsx`）实现 |
| 布局复用           | 需要手动实现                   | 原生支持布局复用                |
| 服务器端渲染（SSR） | 支持                          | 支持，且更灵活                  |

Page Router示例:

```bash
/pages
  /about.js           // 路由 /about
  /blog
    /[id].js          // 动态路由 /blog/:id
```

App Router示例:

```bash
/app
  /about
    /page.tsx         // 路由 /about
  /blog
    /[id]
      /page.tsx       // 动态路由 /blog/:id
  /layout.tsx         // 共享布局
```

> 目前最新版本的nextjs推荐使用App Router的方式, 本文后续也以App Router的方式进行介绍

### 1.3 Layout

在`app`目录中的`layout.tsx`是项目的root layout, 是必须得，且必须包含`<html>`和`<body>`标签。

```typescript
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```

### 1.4 public目录

项目根目录下可选加一个`public`目录，通常用来存放一些静态资产例如图片、字体等。在`public`中的文件可以使用base URL `/`来进行引用。

```typescript
import Image from 'next/image'
 
export default function Page() {
  return <Image src="/profile.png" alt="Profile" width={100} height={100} />
}
```

### 1.5 设置绝对路径imports和module path别名

`Next.js`内置支持`paths`和`baseUrl`选项，这些通常在`tsconfig.json`中设置。

```json
{
  "compilerOptions": {
    "baseUrl": "src/",  // 设置baseUrl为src
    "paths": {
      "@/styles/*": ["styles/*"],
      "@/components/*": ["components/*"]
    }
  }
}
```

### 1.6 项目结构

典型的`Next.js`项目结构如下：

|file name|description|
|---------|-----------|
|app | App Router | 
|public	| Static assets to be served|
|next.config.js	| Configuration file for Next.js |
|package.json	| Project dependencies and scripts |
|instrumentation.ts	| OpenTelemetry and Instrumentation file|
|middleware.ts | Next.js request middleware|
|.env	| Environment variables|
|.env.local	| Local environment variables|
|.env.production	| Production environment variables|
|.env.development	| Development environment variables|
|.eslintrc.json | Configuration file for ESLint|
|.gitignore	| Git files and folders to ignore|
|next-env.d.ts	| TypeScript declaration file for Next.js|
|tsconfig.json	| Configuration file for TypeScript|




## 2. 组件

### 服务端和客户端组件

默认情况，layouts和pages是`Server Components`, 允许在服务器上获取数据并渲染部分UI, 并且可以选择缓存结果然后将其流式传输到客户端。当您需要交互功能或浏览器 API 时，可以使用`Client Components`客户端组件。

什么时候选择客户端组件`Client Components`?

- 状态和事件处理程序，例如: `onChange`, `onClick`
- 生命周期逻辑Lifecycle logic, 例如：`useEffect`
- 仅限于浏览器的API, 例如: `localStorage`, `window`等
- Custom Hooks

什么时候选择服务器组件`Server Components`?

- 从API或者数据库获取数据
- 使用API密钥、令牌等，且不暴露给客户
- 减少发送到浏览器的Javascript数量
- 优化首次内容绘制（First Contentful Paint, FCP）, 并将内容逐步传输到客户端

下面的示例中：`<Page>`是一个服务器组件，它获取的数据并按照props传递到`<LinkButton>`处理客户端交互。

```typescript
// app/[id]/page.tsx
import LikeButton from '@/app/ui/like-button'
import { getPost } from '@/lib/data'
 
export default async function Page({ params }: { params: { id: string } }) {
  const post = await getPost(params.id)
 
  return (
    <div>
      <main>
        <h1>{post.title}</h1>
        {/* ... */}
        <LikeButton likes={post.likes} />
      </main>
    </div>
  )
}
```

```typescript
// app/ui/like-button.tsx
'use client'
 
import { useState } from 'react'
 
export default function LikeButton({ likes }: { likes: number }) {
  // ...
}
```

## 3. 样式

### 3.1 tailwind


## 4. Auth.js

`Auth.js`是一个基于标准Web API的运行时无关库，可以与多个现代Javascript框架集成，提供了易于上手、方便扩展且私密安全的身份验证体验。

> 后续的介绍基于`next-auth@5.0.0-beta`及以上的版本

使用`Auth.js`验证用户身份的方法有4种：

1. OAuth身份验证（使用Google, Github等登录）
2. 魔术链接Magic Links（电子邮件提供商如Forward Email, Resend等）
3. Credentials (用户名和密码)
4. WebAuthn(Passkeys, etc...)

### Hello, Auth.js

**初始化**

依赖安装：`pnpm add next-auth@beta`
初始化必须的环境变量`AUTH_SECRET`: `pnpm dlx auth secret`, 这会添加对应的环境变量到`.env`文件，或者`Next.js`中的`.env.local`中

**基础配置**

通常会在项目中创建`auth.ts`文件来进行`Auth.js`的配置，在文件中我们将配置的内容传递给框架特定的初始化函数，然后导出路由处理程序、登录和退出方法等。

```typescript
import NextAuth from "next-auth"
 
export const { handlers, signIn, signOut, auth } = NextAuth({
  providers: [],
})
```

然后在`app/api/auth/[...nextauth]`中创建对应的Route Handler。

```typescript
// app/api/auth/[...nextauth]/route.ts
import { handlers } from "@/auth" // Referring to the auth.ts we just created
export const { GET, POST } = handlers
```

最后添加可选的中间件以保持会话处于活动状态，这将在每次调用时更新会话到期时间。

```typescript
// middleware.ts
export { auth as middleware } from "@/auth"
```

**验证**

> Auth.js推荐使用OAuth服务

Auth.js 默认使用加密的 JSON Web Token(JWT) 将会话保存在 Cookie 中，因此您无需设置数据库。如果希望持久保存用户数据，可以使用我们的官方数据库适配器之一设置数据库，或者创建您自己的数据库。

## 5. 数据交互

### 5.1 获取数据Fetching data

Server Components中获取数据常用的方式：

1. `fetch` API

如果需要使用`fetch`获取，需要将组件转换为异步函数，并等待`fetch`调用。

```typescript
// app/blog/page.tsx
export default async function Page() {
  const data = await fetch('https://api.vercel.app/blog')
  const posts = await data.json()
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  )
}
```

> 默认情况下，`fetch`响应不会被缓存，但是`Next.js`会预渲染路由，并将输出缓存以提高性能；如果需要启动动态渲染（dynamic rendering）,需要使用`{cache: 'no-store'}`选项。


2. ORM或者数据库

由于Server Components在服务器上渲染，所以可以安全的使用ORM或者数据库, 将组件转换为异步函数并等待调用。

```typescript
// app/blog/page.tsx
import { db, posts } from '@/lib/db'
 
export default async function Page() {
  const allPosts = await db.select().from(posts)
  return (
    <ul>
      {allPosts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  )
}
```

Client Components获取数据的方式:

1. 使用`use` hook


## 8. React知识拾遗

### 8.1 `Suspense`







