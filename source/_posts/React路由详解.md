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
