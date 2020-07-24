---
title: Webkit架构和模块
categories: 浏览器原理
tags: webkit
date: 2020-06-23 23:50:33
---

## JavaScriptCore 引擎是 Webkit 中的默认 JavaScript 引擎，在 Google 的 Chromium 开源项目中，它被替换为 V8 引擎

## Webkit 整体架构

{% asset_img all-arch.png "Webkit整体架构" %}

## Webkit 源代码结构

webkit 的代码众多，大概超过 500 万行，但是他的目录结构相对清晰，通过目录结构基本上可以了解 Webkit 的功能模块。
在一级目录中，重要的有四个，他们分别是如下，对我们分析来说，Source 最重要

- LayoutTests
- PerformanceTests
- Source
- Tools

Source 目录中的子目录中，重要的目录包括

- JavaScriptCore (默认的 JavaScript 渲染引擎)

  - Platform
  - WebCore
  - Webkit
  - Webkit2
  - WTF （基础类库）

  ## Chromium 模块结构图

{% asset_img   chromium-arch.png "Webkit整体架构" %}

## Chromium 的多进程架构

### Chromium 浏览器主要包括以下进程

- Browser 进程，浏览器的主进程
- Renderer 进程，网页的渲染进程，可能有多个
- NPAPI 插件进程，为 NPAPI 类插件而创建的，
- GPU 进程，最多只有一个，当且仅当 GPU 硬件加速打开的时候才会被创建，主要用于对 3D 图形加速调用的实现
- Pepper 插件进程，为 Pepper 类插件而创建的，
- 其他类型的进程

  {% asset_img   multi_chrom.png "chromium 多进程模型" %}

  如何在支持进程间通信的同时，又能支持高效渲染或者用户事件响应呢？，答案是多线程模型

  ### 多线程模型

  多线程的目的主要是为了保持用户界面的高响应度，保证 UI 线程（Browser 进程中的主线程）不会被任何其他费时的操作的阻碍从而影响了对用户操作的响应。更甚者，为了利用多核的优势，Chromium 将渲染过程管线化，这样可以让渲染的不同阶段在不同的线程执行。

  ### Content

  Content 接口不仅提供了一层对多进程进行渲染的抽象接口，而且从诞生以来一个重要的目标就是要支持所有 HTML5 功能，GPU 硬件加速功能和沙箱机制

  ### Chromium 多线程
