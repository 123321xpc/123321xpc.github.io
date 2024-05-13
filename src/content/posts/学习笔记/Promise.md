---
title: Promise
published: 2024-05-13
description: ''
image: ''
tags: [Promise, 学习笔记]
category: '学习笔记'
draft: true 
---

# 异步编程有哪些

+ fs 文件操作
+ 数据库相关操作
+ AJAX
+ 定时器



# 什么是Promise

`Promise`是``JS`中的一种异步编程的解决方案。其本质是一个`构造函数`，其对象用来封装一个异步操作，并能够获取其成功和失败的结果值。

> 注：没有Promise前，使用回调函数解决异步编程问题。



# Promise优点

1. 支持链式调用，能够解决`回调地狱`问题。
2. 指定回调函数的方式更灵活：`Promise`返回的是对象，对象的可操作性比单纯的回调函数高得多。



# Promise基本流程

如下图所示：

![QQ截图20240513161629](/writing/Promise.asserts/QQ%E6%88%AA%E5%9B%BE20240513161629.png)



# 基本使用

## 封装语法

```js
// Promise封装异步操作
const p = new Promise((resolve, reject) => {
    // 此处进行异步操作，比如网络请求，定时器等

    setTimeout(() => {
        // 若成功，则调用resolve方法，传入成功的结果
        // 若失败，则调用reject方法，传入失败的原因

        // 例：
        let num = Math.random();
        if (num < 0.5) {    // 假设随机数小于0.5，则成功
            resolve('success');
        } else {           // 否则失败
            reject('error');
        }
    }, 1000);
});

// 之后可以对对象p进行操作
p.then(res => alert('成功：' + res), 
err => alert('失败：' + err))
```



## Promise封装文件读取操作

要求：读取同目录下的`text.txt`文件中的内容。代码如下：

 ```js
// 引入文件读取模块
const fs = require('fs');

const p = new Promise((resolve, reject) => {
    // 异步读取文件
    fs.readFile('./text.txt', (err, data) => {
        // 若出错，则 reject 返回错误信息
        if(err) reject(err);
        // 若成功，则 resolve 返回文件内容
        else resolve(data.toString());
    })
})

// 查看结果
p.then(data => console.log(data))
.catch(err => console.error(err))
 ```

+ 文件读取成功时，返回如下：

![QQ截图20240513130539](/writing/Promise.asserts/QQ%E6%88%AA%E5%9B%BE20240513130539.png)

+ 文件读取失败时，返回如下：

![QQ截图20240513130634](/writing/Promise.asserts/QQ%E6%88%AA%E5%9B%BE20240513130634.png)



# Promise对象的属性

## PromiseState 状态

`Promise`状态一共有3种：

+ `pending`：未确定
+ `resolved` / `fullfilled`：成功
+ `rejected`：失败

状态改变只有2种可能：

+ `pending -> resolved`
+ `pending -> rejected`



## PromiseResult 结果

保存着异步任务成功 / 失败的结果



# API

## Promise.resolve（value）

作用：返回一个Promise对象，若`value`不是`Promise`类型，均返回成功状态的`Promise`；若`value`为`Promise`对象，则与其状态一致。

如下例子所示：

```js
const p1 = Promise.resolve(42);  // 返回成功的Promise对象
console.log(p1);

const t = new Promise((resolve, reject) => reject('失败'));
const p2 = Promise.resolve(t);  // 返回失败的Promise对象
console.log(p2);
```

运行结果如下：

![QQ截图20240513163507](/writing/Promise.asserts/QQ%E6%88%AA%E5%9B%BE20240513163507.png)



## Promise.reject(value)

作用：返回一个失败的`Promise`对象，无论参数为何类型。即使传入成功的`Promise`对象，也返回失败。



## Promise.all（promises）

+ 传入参数：`Promise`数组。

+ 返回参数：`Promise`对象。
+ 只有数组中所有`Promise`对象的结果均为成功，返回的对象才会是成功，并且返回数据是储存了所有成功信息的数组。如下所示：

```js
		// p1, p2, p3 均为成功的Promise
        const p1 = Promise.resolve(1);
        const p2 = Promise.resolve(2);
        const p3 = Promise.resolve(3);

        const p4 = Promise.all([p1, p2, p3]);  // 返回成功对象
        console.log(p4);
```

返回结果如下：

![QQ截图20240513164649](/writing/Promise.asserts/QQ%E6%88%AA%E5%9B%BE20240513164649.png)



+ 若有对象失败，则返回失败的`Promise`对象，数据为`第一个`失败对象的失败信息。如下所示：

```js
		//p2, p3 均为失败的Promise
        const p1 = Promise.resolve(1);
        const p2 = Promise.reject(2);
        const p3 = Promise.reject(3);

        const p4 = Promise.all([p1, p2, p3]);  // 返回失败对象，数据为2
        console.log(p4);
```

返回结果如下：

![QQ截图20240513164838](/writing/Promise.asserts/QQ%E6%88%AA%E5%9B%BE20240513164838.png)



## Promise.race（promises）

+ 传入参数：`Promise`对象数组

