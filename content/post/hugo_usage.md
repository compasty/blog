---
date: '2025-03-19T11:19:58+08:00'
draft: false
title: 'Hugo使用记录'
categories:
  - tech
tags:
  - hugo
keywords:
  - hugo
  - blog
description: 
  - hugo使用和配置
---

# 基础

## Hugo常用命令

```bash
# 创建新站点，指定配置文件格式为yaml, 默认为toml
hugo new site [site_name] --config yaml
# 创建新博文
hugo new post/[xxx].md
# 启动服务
hugo server -D
```

## Hugo目录结构

```
.
├── archetypes
│   └── default.md
├── assets
├── content
├── data
├── layouts
├── static
├── resources
├── themes
└── hugo.yaml
```
| 文件名称    | 简要说明                                                                                                     |
|-------------|--------------------------------------------------------------------------------------------------------------|
| archetypes  | 该文件夹主要用来存储博客生成的模板文件，初次使用只有一个default.md，可以根据个人的主题配置添加自定义头部信息  |
| assets      | 该文件夹主要用于保存博客样式css和js文件                                                                      |
| content     | 保存个人博客所有内容                                                                                        |
| data        | 保存生成站点时候所需要的配置文件                                                                            |
| layouts     | 以.html形式存储模板，将你博客内容呈现为静态页面                                                              |
| static      | 存储所有静态内容：图片、.css、.js等，当使用 Hugo 生成静态页面时，所有内容将会被复制                             |
| resources   | 缓存一些文件来加速站点生成                                                                                   |
| themes      | 保存主题                                                                                                    |
| hugo.yml  | 个人博客主题样式配置文件                                                                                    |

## 主题安装

以本博客使用的[PaperMod](https://github.com/adityatelange/hugo-PaperMod)为例。

安装主题
```bash
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
# 主题更新
git submodule update --remote --merge
```

配置主题，修改`hugo.yaml`的主题配置并调整其他配置

```yaml
theme: ["PaperMod"]
```

## 内容管理

Hugo中写作的内容都是放在`content`目录下的, 参考官方文档[Content Management](https://gohugo.io/content-management/)。

# 配置

