---
title: CSS常用技巧备忘录
date: 2020-04-23 20:54:06
tags: CSS
---
### 布局相关
#### 1、实现 列表label不换换行，内容自适应剩余宽度换行显示

先上实际效果图


{% asset_img layout_label_content.png  实际实现效果 %}

##### 具体结构和样式设置如下

HTML



````html
<div class="parent">
<div class="label">
代表作
</div>
<div class="content">
代表作内容
</div>
</div>
````
CSS

```css
.parent{
    display:flex;
}
.label{
    display: inline-block;
    height: 100%;
    white-space: nowrap;
}
.content{
    display: inline;
    word-wrap: break-word;
    word-break: break-all;
}
```

