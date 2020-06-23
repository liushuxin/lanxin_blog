---
title: 初识Webkit
date: 2020-04-15 23:50:05
categories: 浏览器原理
tags: webkit
---

## 初识 webkit

浏览器是我们 web 开发的伙伴，那么，你真的懂浏览器吗？接下来的文章就让我们一起来认识浏览器内核 webkit

### 1、浏览器特性

一个浏览器应该包含的功能

- 网络
- 资源管理
- 网页浏览
- 多页面管理
- 插件和扩展
- 书签管理
- 历史记录管理
- 设置管理
- 下载管理
- 账户和同步
- 安全机制
- 隐私管理
- 外观主题
- 开发者工具

### 2、HTML

#### 发展历程

- HTML 1.0 1991 年
- HTML 4.0 1997 年
- HTML 4.1 1999 年
- HTML 5.0 2012 年

HTML5 包含了一系列的标准，一共包含了 10 个大的类别

| 类别                     | 具体规范                                                                                    |
| :----------------------- | :------------------------------------------------------------------------------------------ |
| 离线（offline）          | Application cache Local storage Indexed DB,在线/离线事件                                    |
| 连接（connectivity）     | Web Sockets, Server-sent 事件                                                               |
| 文件访问 （file access） | File API,File System,File Writer,ProgressEvents                                             |
| 语义                     | 各种新的元素，包括 Media,structural,国际化，Link relation,属性，form 类型，microdata 等方面 |
| 音频和视频               | HTML5 Video, Web Audio WebRTC,Video track 等                                                |
| 3D 和图形                | Canvas 2D, 3D CSS 变换， WebGL,SVG 等                                                       |
| 展示                     | CSS3 2D/3D 变换 ，转换（transition）,WebFonts 等                                            |
| 性能                     | Web Worker,HTTP caching 等                                                                  |
| 其他                     | 触控和鼠标，Shadow DOM，CSS masking 等                                                      |

### 3、浏览器内核及其特性

#### 内核和主流内核

在浏览器中，有一个<font color="red">最重要</font>的模块，<font color="red">它主要的作用是将页面转变成可视化的图像结果</font>
这就是<font color="red">浏览器内核</font>，通常，它也被称为<font color="red">渲染引擎</font>

目前主流的渲染引擎包括 Trident,Gecko,和 Webkit 他们分别是 IE,火狐和 Chrome 的内核（2013 年 Google 宣布了 Blink 内核,它其实是从 Webkit 复制出去的）

#### 内核特征

根据渲染引擎所提供的渲染网页的功能，它需要包含下图所示的众多功能模块。图上主要分为三层，最上层使用虚线框住的是渲染引擎所提供的功能

{% asset_img neihe.png "渲染引擎模块及其依赖的模块" %}

从图中大致可以看出，一个渲染引擎主要包括

HTML 解释器、CSS 解释器、布局和 JavaScript 引擎等

- HTML 解释器： 解释 HTML 文本的解释器，主要作用是将 HTML 文本解释成 DOM（文档对象模型）树，DOM 是一种文档的表示方法
- CSS 解释器：级联样式表的解释器，它的作用是为 DOM 中各个元素计算出样式信息，从而为计算最后网页的布局提供基础设施
- 布局：在 DOM 创建之后 Webkit 需要将其中的元素对象同样式信息结合起来，计算它们的大小样式等布局信息，形成一个能够表示这所有信息的内部表示模型
- JavaScript 引擎：使用 JavaScript 代码可以修改网页的内容，也能修改 CSS 的信息，JavaScript 引擎能够解释 JavaScript 代码，并通过 DOM 接口和 CSSOM 接口来修改网页内容和样式信息，从而改变渲染的结果
- 绘图：使用图形库将布局计算后的各个网页的节点绘制成图像的结果

在了解了这些主要模块之后，下面介绍这些模块是如何一起工作完成网页的渲染过程，一般的，一个典型网页的渲染过程如下图所示

{% asset_img xuanran.png "典型渲染过程" %}

## WebKit 内核

### Webkit 和 Webkit2

### Chromium 内核：Blink

历史总是惊人的相似，当年发生在 KHTML 上的事情，也同样发生在 Webkit 项目上。2013 年 4 月，Google 宣布从 Webkit 复制出来并独立运作的 Blink 项目。
