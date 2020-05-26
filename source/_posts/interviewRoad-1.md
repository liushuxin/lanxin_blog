---
title: interviewRoad-1
date: 2020-05-20 15:35:52
categories: interview
tags: 日常一问
---

# 问题

## 1、JS 为什么是单线程的? 为什么需要异步? 单线程又是如何实现异步的呢?

相关申引：
这段 setTimeout 代码什么意思? 我们一般说: 3 秒后,会执行 setTimeout 里的那个函数

```javascript
setTimeout(function () {
  console.log("执行了");
}, 3000);
```
