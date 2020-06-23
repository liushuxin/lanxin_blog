---
title: HTML网页和结构
categories: 浏览器原理
tags: webkit
date: 2020-06-16 21:17:34
---

# 网页构成

# 网页结构

## 框结构

frame,frameset,iframe,可以用来在当前网页中嵌入新的框

## 层次结构

网页中的层次结构指，网页中的元素可能分布在不同的层次中，
对于需要复杂变换和处理的元素，他们需要新层,所以，Webkit 为他们构建新层，其实是为了<font color="red">渲染引擎在处理上的方便和高效</font>
但是对于不同的渲染引擎，他们的策略可能不一样，哪怕是同一渲染引擎不同浏览器分层策略也有可能不一样，后续我们会拿 Chromium 上来讲解

## Webkit 的网页渲染过程

浏览器的主要作用就是将用户输入的 URL,转变成可视化的图像，这其中包含两个过程

- 网页加载过程：从 URL 到构建 DOM 树
- 网页渲染过程：从 DOM 树到页面图像

这两个过程也会交叉，所以很难给予明确的区分，

### Webkit 的渲染过程

<font color="red">根据数据的流向，这里将渲染过程分成三个阶段</font>

1. 从网页的 URL 到构建完 DOM 树
2. 从 DOM 树 到构建完 Webkit 的绘图上下文
3. 从绘图上下文到生成最终的图像

#### 一、从网页 URL 到 DOM 树

{% asset_img render1.png "从网页URL 到DOM 树" %}

涉及两个事件：(对应 Performance 中两条竖线)

- DOMContentLoaded（DOM 已经创建完成）
- onLoad （资源都加载完成）

#### 二、Webkit 利用 CSS 和 DOM 树构建 RenderObject 树直到绘图上下文

{% asset_img render2.png "利用 CSS 和 DOM 树到绘图上下文" %}

#### 三、根据绘图上下文来生成最终的图像

{% asset_img render3.png "根据绘图上下文来生成最终的图像" %}

### 注意：

上面介绍的是一个完整的渲染过程，现代网页很多都是动态的，这意味着在渲染之后，由于网页的动画和用户的交互，浏览器其实<font color="red">一直在不停地重复执行渲染过程</font>
