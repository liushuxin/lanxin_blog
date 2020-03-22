---
title: React路由详解
tags: React-Router
categories: React
date: 2020-03-15 12:01:07
---

## React Router 哲学

&emsp;&emsp;在构建单页面应用时，我们需要用到路由，来决定不同的 URL 跳转到不同的页面，而 React 的思想是以组件化的形式来构建页面，所以 React Router 是根据不同的 URL 跳转到不同的组件。

&emsp;&emsp;对于绝大部分框架来说，路由都是静态的，react-router 在 pre-v4 之前也是静态的，但是之后改为动态路由
动态路由是应用程序渲染时发生的路由

## 基本组件

React Router 中有三种类型的组件

1. router components
2. route matching components
3. navigation components

### 路由

&emsp;&emsp;React Router 中有三种类型的组件： router components, route matching components，和 navigation components。你在 Web 应用程序中使用的所有组件都应该从 react-router-dom 中导入。import { BrowserRouter, Route, Link } from "react-router-dom";
路由

&emsp;&emsp;每个 React Router 应用程序的核心应该是一个 router 组件。对于 Web 项目，react-router-dom 提供了 <BrowserRouter> 和 <HashRouter> 路由。这两个路由都会为你创建一个 <font color="red">专门的 history 对象</font> 。一般来说，如果你有一个<font color="green">响应请求的服务器</font> ，则你应该使用 <font color="green">&lt;BrowserRouter&gt;</font>如果你使用的是<font color="#00FFFF">静态文件的服务器</font>，则应该使用<font color="#00FFFF">&lt;HashRouter&gt;</font>。

### Route 匹配

有两个路由匹配组件： &lt;Route&gt; 和 &lt;Switch&gt;

&emsp;&emsp;路由匹配是通过比较 &lt;Route&gt; 的 <font color="red">path</font> 属性和 <font color="red">当前地址的 pathname</font> 来实现的。当一个 &lt;Route&gt; 匹配成功时，它将渲染其内容，当它不匹配时就会渲染 null。没有路径的 &lt;Route&gt; 将始终被匹配。

你可以在任何你希望根据地址渲染内容的地方添加 &lt;Route&gt; 。列出多个可能的 &lt;Route&gt; 并排列出来往往很有意义。&lt;Switch&gt;用于将 &lt;Route&gt;分组

&emsp;&emsp; &lt;Switch&gt; 不是分组 &lt;Route&gt;所必须的，但他通常很有用。 一个 &lt;Switch&gt;会遍历其所有的子 &lt;Route&gt;元素，并仅渲染与当前地址匹配的第一个元素。这有助于多个路由的路径匹配相同的路径名，当动画在路由之间过渡，且没有路由与当前地址匹配（所以你可以渲染一个 “404” 组件）

### 路由渲染属性

你有<font color="red">三个属性</font> 来给 &lt;Route&gt;渲染组件:<font color="red">component </font> ，<font color="red">render</font> ，<font color="red">children</font> 。你可以查看 &lt;Route&gt; 文档 来了解它们的更多信息，但在这我们将重点关注 component 和 render 因为这几乎是你总会用到的两个

### 导航

React Router 提供了一个&lt;Link&gt; 组件来在你的应用程序中创建链接。无论你在何处渲染一个 &lt;Link&gt; ，都会在应用程序的 HTML 中渲染锚 （&lt;a&gt;）

&lt;NavLink&gt;是一种特殊类型的 &lt;Link&gt; 当它的 to 属性与当前地址匹配时，可以将其定义为“活跃的”

当你想强制导航时，你可以渲染一个 &lt;Redirect&gt;。当一个 &lt;Redirect&gt; 渲染时，它将使用它的 to 属性进行定向
