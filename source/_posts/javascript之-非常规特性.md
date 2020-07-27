---
title: javascript之-非常规特性
categories: JavaScript
tags: base
date: 2020-06-04 22:07:05
---

## 1、假值

| 值              | 类型      |
| :-------------- | :-------- |
| 0               | Number    |
| NaN（非数值）   | Number    |
| “” （空字符串） | String    |
| false           | Boolean   |
| null            | Object    |
| undefined       | Undefined |

## Number.EPSILON

在 javascript 中比较两个浮点数的运算
正确的比较方法是使用 JavaScript 提供的最小精度值

```javascript
Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON;
```

检查等式左右两边差的绝对值是否小于最小精度，才是正确的比较浮点数的方法。这段代码结果就是 true 了。
