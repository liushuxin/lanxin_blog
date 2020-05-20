---
title: JavaScript 事件循环(event loop)
date: 2020-05-20 14:31:32
categories: javascript基础
tags: JavaScript
---

### JavaScript 事件循环(event loop)

javascript 里将任务分为同步任务和异步任务

按照这种分类方式:JS 的执行机制是:

- 首先判断 JS 是同步还是异步,同步就进入主线程,异步就进入 event table
- 异步任务在 event table 中注册函数,当满足触发条件后,被推入 event queue
- 同步任务进入主线程后一直执行,直到主线程空闲时,才会去 event queue 中查看是否有可执行的异步任务,如果有就推入主线程中
  以上三步循环执行,这就是 event loop

  ##### 然而存在另一种划分任务的方式：

- macro-task(宏任务)：包括整体代码 script，setTimeout，setInterval

- micro-task(微任务)：Promise，process.nextTick

按照这种分类方式:JS 的执行机制是

执行一个宏任务,过程中如果遇到微任务,就将其放到微任务的【事件队列】里

当前宏任务执行完成后,会查看微任务的【事件队列】,并将里面全部的微任务依次执行完
