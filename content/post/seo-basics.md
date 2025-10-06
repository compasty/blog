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

# 技术SEO: Technical SEO

## 常见优化

1. 使用HTTPS
2. 查找并修复重复内容
3. 确保用户和爬虫只访问网站的一个版本：也就是不要让`https://yourwebsite.com`和`https://www.yourwebsite.com`不要同时出现在索引中，建议使用一个版本然后将另一个版本重定向到主网站上。
4. 提高页面访问速度: 常见的优化方式有压缩图像（使用ShortPixel等优化工具）、使用CDN, 压缩HTML/CSS/JS文件等
5. 确保移动访问体验：Google是移动索引优先mobile-first indexing
6. 使用Breadcrumb导航：breadcrumb是文本链接的轨迹，可向用户显示他们在网站上的位置以及他们如何到达该点
7. 分页Pagination代替无限滚动：方便google加载
8. 使用结构化标记structured data markups：<https://developers.google.com/search/docs/appearance/structured-data/search-gallery>
9. 如果网站有多语言内容，需要使用[hreflang tags](https://www.semrush.com/blog/hreflang-attribute-101/)

## Core Web Vitals

参考：<https://developers.google.com/search/blog/2020/11/timing-for-page-experience>

Core Web Vitals 是 Google 用来衡量用户体验的速度指标，这些指标包括：

1. LCP(Largest Contentful Paint): 计算网页为用户 加载其最大元素所花费的时间, 建议**2.5 秒或更短**
2. FID(First Input Delay): 衡量对用户与网页的首次交互做出反应所需的时间，建议**100 毫秒或更短**
3. CLS(Cumulative Layout Shift): 测量网页上各种元素的布局的意外偏移，建议**0.1 或更低**

## sitemap&robots.txt

sitemap列出了网站上希望搜索引擎希望索引的重要页面， 通常位于如下位置：`[site.com]/sitemap.xml`或者`[site.com]/sitemap_index.html`。

## Meta viewport tags

## hreflang-attribute

## Canonical URL

<https://www.semrush.com/blog/canonical-url-guide/>

## 常见google命令

### `site:`命令

1. `site:`接网站名可以查看索引的页面数量：例如`site:www.semrush.com`

![Site command with site name](/images/tech/site_cmd_whole.png)

2. `site:`接详细URL可以确认对应页面是否被索引, 例如：`site:www.semrush.com/blog/what-is-seo`

![Site command with specific url](/images/tech/site_cmd_specific_url.png)

常见问题

1. 孤立页面orphaned pages:

# Google相关操作

## GSC提交

可以将网站提交到[Google Search Console](https://search.google.com/search-console/about)使Google搜索引擎进行检索

这个网站可以查看“Core Web Vitals” report

[Submit Sitemap](https://www.semrush.com/blog/submit-sitemap-to-google/)

## Google PageSpeed Insights

<https://pagespeed.web.dev/>

除了查看访问速度，还可以查看网站是否适合移动访问，例如：

1. Meta viewport tags: 告诉浏览器如何控制页面可见区域大小的代码
2. 清晰的字体大小
3. 按钮和可点击元素周围是否有足够的间距等

![PageSpeed insights mobile detections](/images/tech/psi_mobile_detect.png)

## Google Analytics

# 外链建设

# 常用网站和插件

## Semrush

1. 站点审核工具[SiteAudit](https://www.semrush.com/siteaudit/): 审查识别网站中的技术性SEO问题：如重复内容，孤立页面等
2. 页面SEO检查器[On Page SEO Checker](https://www.semrush.com/on-page-seo-checker/)

## Yoast

## RankMath

# 常用名词

1. TLD: Top-level domain顶级域名
2. GSC: Google Search Console

# 参考

1. [SEO Guide](https://ahrefs.com/blog/seo-basics/)
