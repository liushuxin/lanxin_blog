---
title: javascript中的函数
date: 2020-02-16 13:14:49
categories: javascript基础
tags: JavaScript
---

### 函数对象

javascript 中函数就是对象，对象是 名/值对的集合。并拥有一个连接到原型对象的隐藏连接。对象字面量产生的对象连接到 Object.prototype ,函数对象连接到 Function.prototype (该原型对象的本身连接到 Object.prototype)
每个函数在创建时会附加两个隐藏属性，函数的上下文和实现函数的代码

```
Function.prototype.**proto** == Object.prototype
result:true
```

每个函数在创建时也随配有一个 prototype 属性，该属性是一个拥有 constructor 属性，且值即为该函数的对象。
这和隐藏连接到 Function.prototype 完全不同。
函数的与众不同在于他们可以被调用
调用一个函数会暂停当前函数的执行，传递控制权和函数到新的函数。除了声明时定义的形式参数外，每个函数还附加接受两个参数。this 和 arguments 两个参数

### javaScript 中函数的调用模式共分为 4 种：

#### 方法调用模式

在对象中调用自身属性的方法，

```
var object = {
name:"nihao",
method:function(){
console.log("name:"+this.name);
}
}
调用时：object.method();
result: name:nihao
```

#### 函数调用模式

最普遍调用函数的模式：

```
function myfun(a,b){
var c = a +b;
console.log(c);
}
调用：myfun(23,45);
result:68
```

#### 构造器调用模式

如果在函数前面加一个 new 来调用，那么背地里将会创建一个连接到该函数的 prototype 成员的新对象，同时 this 将会被绑定到那个新对象上。

```
var Quo =function(string){
this.status = string;
}
Quo.prototype.get_stauts(){
return this.status;
}
var quo = new Quo("my quo");
console.log(quo.get_stauts());
result:my quo
```

#### Apply 调用模式

因为 javaScript 是一门函数式的面向对象编程语言，因此函数也可以有方法，
apply 方法让我们构建一个参数数组传递给调用函数，它也允许我们选择 this 值。

```
var array =[3,4];
var sum = add.apply(null,array);
var statusObject = {
status:"A-OK"
};
Quo.prototype.get_status.apply(statusObject);
result:A-OK
```

### 参数

当函数被调用时，会得到一个免费配送的参数。那就是 arguments 数组,函数可以通过 arguments 来访问所有它在被调用的时候传递给它的所有参数。包括那些没有在函数定义时分配给函数的参数。这使得编写一个无需指定参数个数的函数成为可能。
因为语言设计的错误，arguments 并不是一个真正的数组，他只是一个类似（array-like）数组的对象。它有一个 length 属性，但它没有任何数组的方法。

### 返回

当一个函数被调用时，它从第一个语句开始执行，并在遇到关闭函数体的 } 时结束。然后函数把控制权交给调用该函数的程序。
return 语句用来使函数提前返回。当 return 被执行时，函数立即返回，而不去执行下面的语句
一个函数总会返回一个值，如果没有指定，则返回 undefined
如果函数在调用时在前面加上了一个 new 前缀。且返回值不是一个对象。则返回 this(该新对象)

### 异常

javascript 提供了一套异常处理机制，异常是干扰程序正常执行的不寻常的事故。你的程序应该抛出一个异常

```
var add function(a,b){
if(typeof a !== 'number' || typeof b !== 'number'){
throw {
name:"TypeError",
message:"add need number"
}
}
return a+b;
}
```

throw 语句中断函数的执行，它应该抛出一个 exception 对象，该对象包含一个用来识别类型的 name 属性和用来描述错误信息的 message 属性。亦可以添加其他属性。
该对象将被传递到一个 try 语句的 catch 从句，如果 try 代码中抛出了异常。控制权就回跳转带 catch 从句。

```
try{
//代码块
}catch(e){
//e:即为抛出的异常
console.log(e.message);
}
```

### 递归

### 作用域

### 闭包

### 模块

### 记忆

### 其他

### 扩充类型的功能，回调，级联，柯里化
