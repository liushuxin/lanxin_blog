---
title: React系列之-事件代理
categories: React
tags: 事件代理
date: 2020-06-04 22:44:35
---

## 事件代理

&emsp;&emsp; React 将事件统一化，使事件在不同浏览器上有一致属性，其内部通过合成事件（SyntheticEvent）的实例传递。如果处于某些原因想使用浏览器原生事件，可以通过 nativeEvent，属性获取。
每个合成事件都有以下属性

- boolean bubbles
- boolean cancelable
- DOMEventTarget currentTarget
- boolean defaultPrevented
- Number eventPhase
- boolean isTrusted
- DOMEvent nativeEvent
- void preventDefault()
- void stopPropagation()
- DOMEventTarget target
- Date timeStamp
- String type

React 支持的事件：
 下面的事件处理程序在事件冒泡阶段被触发，如果要注册事件捕获处理程序，应该使用事件 Capture 事件，所以应该使用 onClickCapture,处理点击事件的捕获阶段，而不是 onClick
