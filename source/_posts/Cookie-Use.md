---
title: Cookie在应用中的使用
categories: JavaScript
tags: cookie
date: 2020-06-04 22:40:19
---

## 基本概念

&emsp;&emsp;Cookie 是服务器保存在浏览器的一小段文本信息，每个 Cookie 的大小一般不能超过 4KB。浏览器每次向服务器发出请求，就会自动附上这段信息，
浏览器可以设置不接受 Cookie,也可以设置不向服务器发送 Cookie
window.navigator.cookieEnabled 返回一个 Boolean 值表示浏览器是否打开 Cookie 功能。

Cookie 主要用在以下三个方面:

1. 会话状态管理（如用户登录状态、购物车）
2. 个性化设置（如用户自定义设置）
3. 浏览器行为跟踪（如跟踪分析用户行为）
