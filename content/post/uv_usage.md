---
date: '2025-03-23T12:44:57+08:00'
draft: false
title: '使用 uv：Python 的极速包管理工具'
categories:
  - tech
keywords:
  - python
  - uv
tags:
  - python
  - uv
---

# 基础

## 什么是 uv？

**uv** 是由 [Astral](https://astral.sh/)（知名 Python 工具 [Ruff](https://github.com/astral-sh/ruff) 的开发者）推出的新一代 Python 包管理工具。它用 Rust 编写，旨在提供**极速的依赖解析和安装体验**，同时兼容现有 Python 工具链（如 `pip` 和 `pip-tools`）。根据官方基准测试，uv 的性能可达传统工具的 10-100 倍。

---

## uv 的核心特点

### 1. ⚡ 极致速度
- 基于 Rust 实现的依赖解析器，速度显著快于传统 Python 工具
- 支持并行下载和缓存机制
- 在大型项目中（如 NumPy），安装速度可提升 **80 倍**

### 2. 🔄 无缝兼容
- 完全兼容 `pip` 和 `pip-tools` 的命令行接口
- 支持 `pyproject.toml` 和 `requirements.txt`
- 可替代 `virtualenv`/`venv` 管理虚拟环境

### 3. 🌐 跨平台支持
- 支持 Windows/macOS/Linux
- 无需 Python 环境即可独立运行

### 4. 🔒 生产级可靠
- 内置依赖版本锁定功能
- 支持生成确定性的依赖清单

### 5. 🧩 可扩展架构
- 提供 Python API 和 Rust API
- 可集成到其他工具链中

---

## 安装 uv

```bash
# On macOS and Linux.
curl -LsSf https://astral.sh/uv/install.sh | sh
# On Windows.
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
## 也可以通过pipx
pipx install uv
```

升级到最新版本：
```bash
# 使用独立安装器
uv self update
# 如果使用pipx安装
pipx upgrade uv
```

---

## 基础使用

### 安装依赖包
```bash
# 从 requirements.txt 安装
uv pip install -r requirements.txt

# 安装单个包（等效于 pip install）
uv pip install requests

# 安装开发依赖
uv pip install -e ".[dev]"
```

### 虚拟环境管理
```bash
# 创建虚拟环境
uv venv .venv

# 激活环境（Windows）
.venv\Scripts\activate

# 激活环境（Unix/macOS）
source .venv/bin/activate
```

### 生成确定依赖
```bash
# 生成锁定文件
uv pip compile requirements.in -o requirements.txt

# 同步依赖（类似 pip-sync）
uv pip sync requirements.txt
```

---

## 实战工作流示例

### 场景：初始化项目
```bash
# 创建并激活虚拟环境
uv venv .venv
source .venv/bin/activate

# 安装开发依赖
uv pip install black ruff pytest

# 生成确定版本清单
uv pip freeze > requirements.txt
```

### 场景：CI/CD 优化
```bash
# 极速安装依赖（利用缓存）
uv pip install -r requirements.txt --cache-dir ./pip-cache

# 并行安装模式
UV_PIP_INSTALL_PARALLEL=true uv pip install -r requirements.txt
```

---

## 进阶功能

### 1. 替换传统工具链
```bash
# 替代 pip
alias pip=uv pip

# 替代 pip-tools
uv pip compile requirements.in  # 替代 pip-compile
uv pip sync requirements.txt   # 替代 pip-sync

# 替代 virtualenv
uv venv  # 比 python -m venv 快 80 倍
```

### 2. 依赖分析
```bash
# 查看依赖树
uv pip list --tree

# 检查安全漏洞
uv pip audit
```

### 3. 跨平台部署
```bash
# 生成跨平台依赖文件
uv pip compile requirements.in --platform linux --python-version 3.10
```

## 总结

