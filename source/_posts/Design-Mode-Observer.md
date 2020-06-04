---
title: JavaScript观察者模式（发布订阅模式）
categories: 设计模式
tags: designMode
date: 2020-06-04 21:59:47
---

## 实现示例

```javascript
var eventuality = function (that) {
  var registry = {};
  //触发事件
  that.fire = function (event) {
    var array,
      func,
      handler,
      i,
      type = typeof event === "string" ? event : event.type;
    if (registry.hasOwnProperty(type)) {
      array = registry[type];
      for (i = 0; i < array.length; i += 1) {
        handler = array[i];
        func = handler.method;
        if (typeof func === "string") {
          func = this[func];
        }
        func.apply(this, handler.parameters || [event]);
      }
    }
    return this;
  };
  that.on = function (type, method, parameters) {
    var handler = {
      method: method,
      parameters: parameters,
    };
    if (registry.hasOwnProperty(type)) {
      registry[type].push(handler);
    } else {
      registry[type] = [handler];
    }
    return this;
  };
  return that;
};
var objectEventTest = {
  a: 1,
  b: 2,
  getA: function () {
    console.log(this.a);
  },
  getB: function () {
    console.log(this.b);
  },
  showC: function (c) {
    console.log(c);
  },
};
eventuality(objectEventTest);
objectEventTest.on("show", "getA");
objectEventTest.on("show", "getB");
objectEventTest.on("show1", "showC", ["show C!!"]);
objectEventTest.fire("show");
```
