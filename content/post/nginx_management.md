---
date: '2025-03-20T13:39:14+08:00'
draft: false
title: 'Nginx日常管理'
categories:
  - tech
keywords:
  - nginx
tags:
  - nginx
description: "Nginx日常管理记录"
---

# 概述

[nginx](https://nginx.org/)是一个高性能的HTTP和反向代理web服务器。

## 安装

参考: https://nginx.org/en/linux_packages.html#Ubuntu

## 使用Let's Encrypt进行SSL处理

参考：https://www.nginx.com/blog/using-free-ssltls-certificates-from-lets-encrypt-with-nginx/

1. 安装Let's encrypt的客户端 certbot

```bash
$ sudo apt-get update
$ sudo apt-get install certbot
$ sudo apt-get install python3-certbot-nginx
```

2. 配置

# 命令

1. 查看版本号: `nginx -v`
2. 停止nginx: `nginx -s stop`
3. 启动nginx: `sudo systemctl restart nginx` 或者 `sudo service nginx restart`
4. 重加载: `nginx -s reload`
5. 测试nginx配置: `nginx -t`

# 配置

nginx的配置文件一般放在conf目录中，配置信息一般主要分为三块

1. 全局块
2. events块
3. http块



