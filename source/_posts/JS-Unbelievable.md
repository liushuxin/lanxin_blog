---
title: JS-Unbelievable
categories: JavaScript
tags: base
date: 2020-06-04 22:24:08
---

### 变量提升

&emsp;&emsp; 1、将变量声明提升到它所在作用域的最开始的部分
变量提升导致以下输出结果并不是我们认为的那样

```javascript

var tmp = new Date();

function f() {
console.log(tmp);
if (false) {
var tmp = ‘hello world’;
}
}
f();

```

输出结果 undefined ,惊不惊喜，意不意外。
