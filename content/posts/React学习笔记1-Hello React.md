---
title: "React学习笔记1"
date: 2020-02-01T09:38:48+08:00
draft: true
---

# Hello React, Hello JavaScript!

> 千里之行，始于足下。——老子

最近体验了一下著名的前端框架React，用起来特别爽，个人很喜欢。所以准备花一点点时间深入学习一下React。在这里把学习得过程也顺便记录下来。

要学习React的话，先了解一下JavaScript的基础知识是非常有帮助的。JavaScript也是是目前非常火的编程语言，在有了Node.js以后，JS终于可以从前端到后端一统天下了。如果熟悉了JS以后，学习React非常简单。

JS也很简单，基本语法快速浏览一下就差不多了。但是JS作为一门动态语言，也有很多非常有意思得特性。首先看几个React里会用到的JS语法。

## destructing 解构赋值
这是一个很方便的用法：
```
let arr = ['a', 'b'];

let [first, last] = arr;

console.log(first);//a
console.log(last); //b
```

## 数组的复制
在JS中，数组的变量是引用传递，在下面的例子可以测试。

在ES6中，有一个比较快捷的语法x = [...y]可以拷贝一个新的数组。
```
const rows = [0, 1, 2];

const copy = rows;

rows.push(3);

console.log(copy); //0, 1, 2, 3

const deepCopy = [...rows];

console.log(deepCopy); //0, 1, 2, 3

rows.push(4);

console.log(deepCopy); //0, 1, 2, 3
```

## 箭头函数
箭头函数大家就非常熟悉了，在JS中，通过箭头函数能把代码写得非常简洁。

在对象中，有一个细微的地方需要注意，箭头函数默认是没有绑定this的。看下面这个例子：
```
const user = {
    name: 'Jacky',
    sayHello() {
        console.log(`hello, ${this}`);
    }
};

user.sayHello(); // hello, [object Object]


const another = {
    name: 'Andy',
    sayHello: () => console.log(this)
}

another.sayHello(); //{}
```

## 关于this
在JS中的this，和其它的常用的编程语言会有一些不同。
所以很多时候表现会和想象的不同，有时候会不习惯。

好消息是，在React较新的版本中，已经有了react hook, react effect这样一些功能，可以完全替代class的用法，这样可以避免this了。

## 参考阅读

- https://javascript.info/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
