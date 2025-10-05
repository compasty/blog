---
date: '2025-10-03T03:50:43+08:00'
draft: false
title: 'SEO基础'
categories:
  - tech
keywords:
  - SEO
tags:
  - SEO
---

# SEO基础

## 什么是SEO?

SEO(Search Engine Optimization)是优化网站及内容，提高在搜索引擎和AI等的可见度。

SEO包含五个主要步骤：

1. Keyword Research: 关键词研究
2. Content Creation: 内容创建
3. On-Page SEO&structure optimization: 页面搜索引擎优化和结构优化：保持良好的格式、内链和结构化数据，可以使内容清晰且机器可读
4. Links and mentions: 外链维护、品牌提及等
5. Technical SEO: 技术搜索引擎优化, 提升网站范围速度/移动端适配/sitemap等

## 事前准备

1. 准备一个好的域名：尽量选择`.com`域名，如果针对指定国家可以使用对应国家的域名
2. 平台选择：托管/自建，主要考虑4S: Secure.Server Location,Support,Search&AI Accessibility
3. 使用`https` + 移动端支持
4. 避免侵入式的弹出窗口和广告

## 创建逻辑站点结构

![site_structure](/images/tech/website_structure.png)

1. 良好的站点结构设计可以使搜索引擎和用户很容易在网站上找到内容，其中内链设计尤为重要（也方便在站点传递PageRank）
2. URL设计也很重要，例如使用wordpress尽量不要使用日期或者数字的格式作为URL,而是使用帖子名称作为URL

## 如何跟踪和衡量SEO性能?

1. 关注自然流量和展示次数Organic Traffic and impressions(这些可以在GSC中查看)
2. 关注关键词排名Keyword Rankings：在Google AI概览中可见对于网站排名也非常重要
3. 关注AI可见性AI visibility

# 关键词Keywords

## 基础

进行关键词研究首先是确定一个“种子关键词”（seed keyword）,然后使用它来生成大量关键词提示，通常可以借助一些关键词工具例如：[Ahrefs keyword generator](https://ahrefs.com/keyword-generator/), [Google Keyword Planner](https://business.google.com/en-all/ad-tools/keyword-planner/), 观察不同关键词的**难易程度和搜索量级**

> 当然也可以借助ChatGPT, 例如：`Suggest 10 short keyword ideas for the following topics: xxx`.

进行关键词研究的第二个方面是要了解关键词意图，例如以咖啡coffee作为主题，准备购买产品或服务的可能搜索：`best instant coffee`,`cuisinant coffee maker`等，这种叫做**商业或者交易关键字(commercial or transactional keywords)**, 还有的搜索：`how much caffeine in coffee`, `coffee cake recipe`这种叫做**信息意图（information intent）**, 还有一些是**导航意图（navigational intent）**, 例如：`coffee near me`.

如何筛选关键字? 通常可以看6个指标：

1. Search Volume: 搜索量。需要注意：（a）这个值是搜索次数，而不是搜索人数（b）不等于你的网站能获得的访问量，即使排位第一，也通常获得不超过30%的流量（c）这是阶段平均值，有的关键词不同时间流量不同
2. Keyword Difficulty: 关键词难度。

# Google网站提交

可以将网站提交到[Google Search Console](https://search.google.com/search-console/about)使Google搜索引擎进行检索

# Google Analytics

# 站内优化

## sitemap&robots.txt

sitemap列出了网站上希望搜索引擎希望索引的重要页面， 通常位于如下位置：`[site.com]/sitemap.xml`或者`[site.com]/sitemap_index.html`。

# 常用网站和插件

## Yoast

## RankMath

# 常用名词

1. TLD: Top-level domain顶级域名
2. GSC: Google Search Console

# 参考

1. [SEO Guide](https://ahrefs.com/blog/seo-basics/)
