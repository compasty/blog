---
date: '2025-03-19T20:22:10+08:00'
draft: false
title: 'Uniswap原理解析'
categories:
  - crypto
tags:
  - Uniswap
keywords:
  - Uniswap
description: "Uniswap原理解析"
---

# 开始

## Uniswap基础

Uniswap 是一个去中心化交易所 (Decentralized exchange, DEX), 旨在成为中心化交易所的替代品。它在以太坊区块链上运行，完全自动化：没有管理员、经理或具有特权访问权限的用户。

Uniswap版本:
1. V1: 2018年11月推出，仅允许以太币和代币之间的兑换
2. V2: 2020年3月推出, 允许任何`ERC20`代币之间直接交换，以及任何对之间的链式交换
3. V3: 2021年5月推出，显著提高了资本效率，这使得流动性提供者可以从池中移除更大一部分流动性，同时仍然获得相同的回报

Uniswap核心是底层自动做市商（automated market maker，AMM）算法，可以创建池子，或者代币对，并填充流动性，让用户利用这些流动性来交换代币。DEX 必须拥有足够（或大量）的流动性才能正常运作，Uniswap的解决方案是**允许任何人成为做市商(allow anyone to be a market maker)**，任何用户都可以将他们的资金存入交易对（并从中受益）。

Uniswap 扮演的另一个重要角色是价格预言机。价格预言机是一种从中心化交易所获取代币价格并将其提供给智能合约的服务。Uniswap 充当二级市场（secondary market），吸引套利者（arbitrageurs）利用 Uniswap 和中心化交易所之间的价格差异获利。这使得 Uniswap 池的价格尽可能接近大型交易所的价格。如果没有适当的定价和储备平衡功能，这是不可能的。

## 恒定乘积做市商Constant product market maker

Uniswap的核心是恒定乘积函数：$x * y = k$, 其中$x$是 ether 储备， $y$是 token 储备（反之亦然），$k$是常数。Uniswap 要求，无论 $x$ 或 $y$的储备有多少，$k$都保持不变。当您用 ether 换取 token 时，您会将 ether 存入合约并获得一定数量的 token 作为回报。Uniswap 确保每次交易后 $k$ 保持不变（事实并非如此，我们稍后会了解原因）。

此外该公式还负责定价计算。

# 实现V1版本


# 参考

1. [Uniswap V3 Book](https://y1cunhui.github.io/uniswapV3-book-zh-cn/)
2. [Programming Defi: Uniswap](https://jeiwan.net/posts/programming-defi-uniswap-1/)