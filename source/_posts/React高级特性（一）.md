---
title: React高级特性（一）
date: 2020-04-30 21:57:57
categories: React
tags: React高级特性
---

### 1、React.StrictMode

&emsp;&emsp;是一个用来突出显示应用程序中<font color="red">潜在问题 </font>的工具，StrictMode 不会渲染任何可见的 UI，它为其后代元素触发额外的<font color="red">检查和警告 </font>

_注意：严格模式检查仅在开发模式下运行；它们不会影响生产构建。_

StrictMode 目前有助于：

1. 识别不安全的生命周期
2. 关于使用过时字符串 ref API 的警告
3. 关于使用废弃的 findDOMNode 方法的警告
4. 检测意外的副作用
5. 检测过时的 context API

**未来的 React 版本将添加更多额外功能。**

### 2、Portals

Portal 提供了一种将子节点渲染到存在于父组件以外的 DOM 节点的优秀的方案

```javascript
ReactDOM.createPortal(child, container);
```

第一个参数（child）是任何可渲染的 React 子元素，例如一个元素，字符串或 fragment。第二个参数（container）是一个 DOM 元素。

一个 portal 的典型用例是当父组件有 overflow: hidden 或 z-index 样式时，但你需要子组件能够在视觉上“跳出”其容器。例如，对话框、悬浮卡以及提示框

```javascript
import React from "react";
import {createPortal} from "react-dom";

class Dialog extends React.Component {
  constructor() {
    super(...arguments);

    const doc = window.document;
    this.node = doc.createElement("div");
    doc.body.appendChild(this.node);
  }

  render() {
    return createPortal(
      <div class="dialog">{this.props.children}</div>, //塞进传送门的JSX
      this.node //传送门的另一端DOM node
    );
  }

  componentWillUnmount() {
    window.document.body.removeChild(this.node);
  }
}
```

### 3、Error Boundaries（错误边界）

&emsp;&emsp;部分 UI 的 JavaScript 错误不应该导致整个应用崩溃，为了解决这个问题，React 16 引入了一个新的概念 —— 错误边界

