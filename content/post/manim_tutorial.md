---
date: '2025-03-23T00:31:22+08:00'
draft: false
title: 'Manim使用入门'
categories:
  - Math
keywords:
  - Manim Tutorial
tags:
  - Manim Tutorial
description: "Manim使用入门"
---

# 概述

> 本文使用的是社区版本[manim](https://github.com/ManimCommunity/manim), 文档链接为: https://docs.manim.community/en/stable/

## Manim是什么？

传统上，将技术概念制作成动画是相当繁琐的，因为很难使动画足够精确地传达这些概念。Manim 依靠 Python 的简单性以编程方式生成动画，从而可以方便地指定每个动画的运行方式。

# Manim基础使用

## Hello, Manim

安装参考: [Installing Manim locally](https://docs.manim.community/en/stable/installation/uv.html)

下面是实现绘制一个圆形的代码

```python
from manim import *
class SquareToCircle(Scene):
    def construct(self):
        circle = Circle()  # create a circle
        circle.set_fill(PINK, opacity=0.5)  # set color and transparency

        square = Square()  # create a square
        square.rotate(PI / 4)  # rotate a certain amount

        self.play(Create(square))  # animate the creation of the square
        self.play(Transform(square, circle))  # interpolate the square into the circle
        self.play(FadeOut(square))  # fade out animation
```

然后我们可以调用命令`manim -pql main.py CreateCircle`来生成MP4格式的视频, 这个视频会先渲染一个正方形然后变化为圆形（manim的一个强大之处就在于仅用几行代码即可实现复杂且数学密集的动画， 例如在两个几何形状之间进行干净的插值）。

`manim`的核心是创建一个`Scene`, 大多数情况下，编写动画脚本的代码完全包含在 `Scene`类的`construct()`方法中。在 `construct()`中，您可以创建对象、在屏幕上显示它们并为其设置动画。

## manim基本技巧

### 定位`Mobject`

```python
circle = Circle()  # create a circle
square = Square()  # create a square
square.next_to(circle, RIGHT, buff=0.5)  # set the position
```

在上面的代码中，`next_to`是`Mobject`用来定位的方法，这里将`circle`设置为第一个参数，表明将圆圈指定为正方形的参考点，第二个参数用来指定`Mobject`相对于参考点的放置方向（这里设置为`RIGHT`表示定位在右侧，也可以设置为`LEFT`, `UP`, `DOWN`等），最后`buff=0.5`表示在两个对象之间应用了一个距离buffer。

### 使用`.animate`添加动画

`.animate`是`Mobject`实现动画效果的重要方法，将`.animate`添加到修改`Mobject`属性的方法调用之前，该方法将成为可以使用`self.play`播放的动画。

# Manim示例


