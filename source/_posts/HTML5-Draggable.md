---
title: HTML5_Draggable
categories: HTML5
tags: 拖拽
date: 2020-06-09 16:55:17
---

## 拖拽

HTML 拖放（Drag and Drop）接口使应用程序能够在浏览器中使用拖放功能。例如，用户可使用鼠标选择可拖动（draggable）元素，将元素拖动到可放置（droppable）元素，并释放鼠标按钮以放置这些元素。拖动操作期间，可拖动元素会有一个半透明表示跟随着鼠标指针

### 拖拽事件

HTML 的 drag & drop 使用了 DOM event model 以及从 mouse events 继承而来的 drag events 。一个典型的拖拽操作开始于用户选中一个可拖动的（draggable）元素，并将其拖动（鼠标不放开）到一个可放置的（droppable）元素，然后释放鼠标。

### 接口

HTML 的拖拽接口有 DragEvent, DataTransfer, DataTransferItem 和 DataTransferItemList

### DataTransfer

DataTransfer 对象用于保存拖动并放下（drag and drop）过程中的数据。它可以保存一项或多项数据，这些数据项可以是一种或者多种数据类型。关于拖放的更多信息
这个对象可以从所有拖动事件 drag events 的 dataTransfer 属性上获取。

## 基础

### 确定什么是可拖动的

让一个元素被拖动需要添加 draggable 属性，再加上全局事件处理函数 ondragstart，如下面的示例代码所示

```html
<script>
  function dragstart_handler(ev) {
    // Add the target element's id to the data transfer object
    ev.dataTransfer.setData("text/plain", ev.target.id);
  }

  window.addEventListener("DOMContentLoaded", () => {
    // Get the element by id
    const element = document.getElementById("p1");
    // Add the ondragstart event listener
    element.addEventListener("dragstart", dragstart_handler);
  });
</script>

<p id="p1" draggable="true">This element is draggable.</p>
```

### 定义拖动数据

应用程序可以在拖动操作中包含任意数量的数据项。每个数据项都是一个 string 类型，典型的 MIME 类型，如：text/html

每个 drag event 都有一个 dataTransfer 属性，其中保存着事件的数据。这个属性（DataTransfer 对象）也有管理拖动数据的方法。setData() 方法为拖拽数据添加一个项，如下面的示例代码所示：

```javascript
function dragstart_handler(ev) {
  // 添加拖拽数据
  ev.dataTransfer.setData("text/plain", ev.target.innerText);
  ev.dataTransfer.setData("text/html", ev.target.outerHTML);
  ev.dataTransfer.setData(
    "text/uri-list",
    ev.target.ownerDocument.location.href
  );
}
```

### 定义拖动图像

拖动过程中，浏览器会在鼠标旁显示一张默认图片。当然，应用程序也可以通过 setDragImage() 方法自定义一张图片，如下面的例子所示

```javascript
function dragstart_handler(ev) {
  // Create an image and then use it for the drag image.
  // NOTE: change "example.gif" to a real image URL or the image
  // will not be created and the default drag image will be used.
  var img = new Image();
  img.src = "example.gif";
  ev.dataTransfer.setDragImage(img, 10, 10);
}
```

### 定义拖动效果

dropEffect 属性用来控制拖放操作中用户给予的反馈。它会影响到拖动过程中浏览器显示的鼠标样式。比如，当用户悬停在目标元素上的时候，浏览器鼠标也许要反映拖放操作的类型

1. copy 表明被拖动的数据将从它原本的位置拷贝到目标的位置。
1. move 表明被拖动的数据将被移动。
1. link 表明在拖动源位置和目标位置之间将会创建一些关系表格或是连接。

```javascript
function dragstart_handler(ev) {
  ev.dataTransfer.dropEffect = "copy";
}
```

### 定义一个放置区

当拖动一个项目到 HTML 元素中时，浏览器默认不会有任何响应。想要让一个元素变成可释放区域，该元素必须设置 ondragover 和 ondrop 事件处理程序属性，下面的例子通过简单的事件处理展示了如何使用这些属性：

```html
<script>
  function dragover_handler(ev) {
    ev.preventDefault();
    ev.dataTransfer.dropEffect = "move";
  }
  function drop_handler(ev) {
    ev.preventDefault();
    // Get the id of the target and add the moved element to the target's DOM
    var data = ev.dataTransfer.getData("text/plain");
    ev.target.appendChild(document.getElementById(data));
  }
</script>

<p
  id="target"
  ondrop="drop_handler(event)"
  ondragover="dragover_handler(event)"
>
  Drop Zone
</p>
```

### 处理放置效果

drop 事件的处理程序是以程序指定的方法处理拖动数据。一般，程序调用 getData() 方法取出拖动项目并按一定方式处理。程序意义根据 dropEffect 的值与/或可变更关键字的状态而不同

下面的例子展示了一个处理程序，从拖动数据中获取事件源元素的 id 然后根据 id 移动源元素到目标元素：

```html
<script>
  function dragstart_handler(ev) {
    // Add the target element's id to the data transfer object
    ev.dataTransfer.setData("application/my-app", ev.target.id);
    ev.dataTransfer.dropEffect = "move";
  }
  function dragover_handler(ev) {
    ev.preventDefault();
    ev.dataTransfer.dropEffect = "move";
  }
  function drop_handler(ev) {
    ev.preventDefault();
    // Get the id of the target and add the moved element to the target's DOM
    var data = ev.dataTransfer.getData("application/my-app");
    ev.target.appendChild(document.getElementById(data));
  }
</script>

<p id="p1" draggable="true" ondragstart="dragstart_handler(event)">
  This element is draggable.
</p>
<div
  id="target"
  ondrop="drop_handler(event)"
  ondragover="dragover_handler(event)"
>
  Drop Zone
</div>
```

### 拖动结束

拖动操作结束时，在源元素（开始拖动时的目标元素）上触发 dragend 事件。不管拖动是完成还是被取消这个事件都会被触发。dragend 事件处理程序可以检查 dropEffect 属性的值来确认拖动成功与否
