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

使用`pnpm`可以使用命令: `pnpm dlx create-next-app@latest`，或者创建一个使用Tailwind V4和React 19的项目：`pnpm create next-app@canary --tailwind --eslint --typescript --app --no-src-dir`

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
  /(auth)             
    /login            // 路由 /login
      /page.tsx
    /register
      /page.tsx
  /layout.tsx         // 共享布局
```

> 目前最新版本的nextjs推荐使用App Router的方式, 本文后续也以App Router的方式进行介绍

Next.js使用约定式路由：

1. 基础规则: 文件名称和嵌套层级自动映射为URL地址，只有目录下直接包含page文件才会识别为路由
2. 路由组: 通过`(xxx)`语法创建路由组，不会转换为路径，可用于对路由进行分组管理，例如同组路由使用同一套布局
3. 动态路由: 通过`[xxx]`语法可以让多个不同参数的 URL 复用同一个页面，比如 `app/question/[questionId]/page.tsx` 中 questionId 就是动态路由参数，可以匹配 `/question/1`、`/question/2` 等 URL 地址

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
|public | Static assets to be served|
|next.config.js | Configuration file for Next.js |
|package.json | Project dependencies and scripts |
|instrumentation.ts | OpenTelemetry and Instrumentation file|
|middleware.ts | Next.js request middleware|
|.env | Environment variables|
|.env.local | Local environment variables|
|.env.production | Production environment variables|
|.env.development | Development environment variables|
|.eslintrc.json | Configuration file for ESLint|
|.gitignore | Git files and folders to ignore|
|next-env.d.ts | TypeScript declaration file for Next.js|
|tsconfig.json | Configuration file for TypeScript|

## 2. 组件

### 2.1 服务端和客户端组件

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

从上面的示例中，`"use clint"`这个指令表示创建客户端组件，一旦文件被文件标记为 “use client” ， **其所有导入和子组件都被视为 client bundle 的一部分**，不需要将指令添加到用于 Client 端的每个组件中。

如果希望减少客户端Javascript包的大小，尽量仅在必要的组件上使用`"use client"`指令，而不是将UI的大部分标记为客户端组件。例如：下面的`<Layout>`组件主要包含静态元素，仅其中的搜索栏`<Search>`是交互式的，因此将搜索栏声明为Client Components，而其余保持为Server Components

```typescript
// Client Component
import Search from './search'
// Server Component
import Logo from './logo'
 
// Layout is a Server Component by default
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <>
      <nav>
        <Logo />
        <Search />
      </nav>
      <main>{children}</main>
    </>
  )
}
```

### 2.2 工作原理

#### 2.2.1 服务器端

`Next.js`使用React的API来编排渲染，渲染工作按照各个路由段（layouts and pages）拆分为块：其中: Server Components被渲染成一种特殊的数据格式，称为React Server Component Payload（RSC Payload），Client Components和RSC Payload用于**预渲染**HTML.

> RSC Payload: RSC Payload是用于渲染完成的React服务器组件树的紧凑二进制表示（compact binary representation）, React可以在客户端使用这个数据来更新浏览器DOM.RSC Payload包含：Server Components的渲染结果、客户端组件应呈现位置的占位符以及其对Javascript文件的引用，从Server Component传递到Client Component的任何props

#### 2.2.2 客户端

在客户端上，**HTML**用于立即向用户展示路由的快速非交互式预览，**RSC Payload**用于协调 Client 和Server Component树， **JavaScript**用于激活客户端组件并使应用程序具有交互性。

> hydration(补水)：表示React 将事件处理程序附加到 DOM 的过程，以使静态 HTML 具有交互性

### 2.3 数据传递

可以使用`props`将数据从Server Components传递到Client Components（如2.1中的`<LikeButton>`组件）, 也可以使用`use` Hook进行流式的传值。

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

## 5. Shadcn

ShadCN/UI 是一组设计精美、可访问的组件和一个代码分发平台，完全开源。

安装方式：`pnpm dlx shadcn@canary init`
添加组件：`pnpm dlx shadcn@canary add button`

> Shadcn默认使用Tailwind V3, 如果要使用Tailwind V4的话，需要使用`shadcn@canary`, 否则使用`shadcn@latest`

添加组件以后可以类似如下进行使用：

```typescript
import { Button } from "@/components/ui/button"

export default function Home() {
  return (
    <div>
      <Button>Click me</Button>
    </div>
  )
}
```

上面的初始化代码中会创建一个`components.json`文件，其中包含项目的配置。其内容类似如下：

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": false,
  "tsx": true,
  "tailwind": {
    "config": "tailwind.config.ts",
    "css": "src/globals.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": "tw-"
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "iconLibrary": "lucide"
}
```

其中:

1. `schema`: 表示文件对应的json schema
2. `style`: 表示组件的样式，**初始化以后无法更改**
3. `tailwind`: 表示如何在项目中设置Tailand CSS, 其中`config`表示对应的 `tailwind.config.ts`文件所在的路径，**对于Tailwind CSS v4, 该字段应该留空**，`css`表示将Tailwind CSS导入到项目中的文件路径, `baseColor`用于为组件生成默认调色板，**初始化后无法更改**；`cssVariables`表示用CSS变量还是Tailwind CSS utility classes进行主题设置，设置为false表示使用Tailwind CSS utility classes，设置为true表示使用css变量，**初始化后无法更改**；`prefix`用于Tailwind CSS utility classes的前缀。
4. `rsc`表示是否启用对React Server Components的支持，当设置为true时，CLI会自动将`use client`指令添加到客户端组件。
5. `aliases`: shadcn使用这里的配置以及`tsconfig.json`文件中的`paths`配置，来保证生成的组件放置在正确的位置
