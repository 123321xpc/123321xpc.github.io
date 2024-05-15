---
title: Promise 学习笔记
published: 2024-05-13
description: ''
image: ''
tags: [Promise, 学习笔记]
category: '学习笔记'
draft: false 
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

![QQ截图20240513161629](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240513161629.png)



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

![QQ截图20240513130539](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240513130539.png)

+ 文件读取失败时，返回如下：

![QQ截图20240513130634](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240513130634.png)



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

![QQ截图20240513163507](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240513163507.png)



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

![QQ截图20240513164649](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240513164649.png)



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

![QQ截图20240513164838](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240513164838.png)



## Promise.race（promises）

+ 传入参数：`Promise`对象数组
+ 作用：返回数组中最先返回结果的`Promise`对象

例如：

```typescript
  let p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("p1");
    }, 1000);
  });
  
  let p2 = new Promise((resolve, reject) => {
      setTimeout(() => {
          resolve("p2");
      }, 2000);
  });
  
  let p3 = new Promise((resolve, reject) => {     // 最快
      setTimeout(() => {
          reject("p3");
      }, 500);
  });

  console.log(Promise.race([p1, p2, p3]));
```



返回结果如下：

![QQ截图20240514145716](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240514145716.png)



# 一系列问题

## 一、如何改变`Promise`状态？

+ 调用`resolve`和`reject`方法

+ 抛出异常，会变成`reject`状态

## 二、当`Promise`指定多个回调（ promise.then() ）时，是否会全部执行？

+ 若状态为成功状态，均会执行
+ 若为未确定状态，均不会执行

## 三、`Promise`状态改变和回调函数指定谁先谁后？

+ 都有可能，一般是先指定回调函数，后改变状态（因为`Promise`中大多是异步任务）
+ 若想要先改变状态，再指定回调函数，需要在`Promise`中直接调用`resolve` / `reject`方法

## 四、什么时候才能得到数据？

+ 若先指定回调，则状态改变时，回调函数会被调用，得到数据
+ 若先改变状态，则当回调指定时就会被调用，得到数据

## 五、`then`方法返回的结果由什么决定？

**由`then`方法指定的回调函数执行的结果决定。**

> 注意：与原先`Promise`对象结果无关！，具体看第二个例子

- 若回调中抛出错误，则会变为失败，且错误信息为返回数据，具体如下：

```js
const p = Promise.resolve(12);

const res = p.then(res => {throw 'error' },  err => err);
        
console.log(res);
```

其中，`p`返回的是成功的`Promise`，调用`then`方法中的第一个回调函数，但是抛出了错误，**故结果为失败的`Promise`**，如下：

![QQ截图20240515130704](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240515130704.png)





- 若`then`方法中返回结果为一个非`Promise`对象，则返回结果为成功，且值为返回数据，具体如下：

```js
const p = Promise.reject(12);  // p为失败的Promise

const res = p.then(res => {throw 'error' }, err => 33);
        
console.log(res);
```

- 其中，在`then`方法的第二个回调函数中返回`number`类型，返回结果仍为成功的`Promise`，如下：

![QQ截图20240515131225](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240515131225.png)



- 若返回的是`Promise`对象，则由该对象的结果决定。如下：

```js
const p = Promise.resolve(12);  // p为成功的Promise

const res = p.then(res => {throw 'error' }, err => Promise.reject(22));
        
console.log(res);
```

返回结果如下：

![QQ截图20240515131613](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240515131613.png)



## 六、如何实现`Promise`的链式调用？

```js
		const p = Promise.resolve(12);  // p为成功的Promise

        p.then(res => {
            console.log(res);  // 输出12
            return Promise.reject('error');  // 返回一个失败的Promise
        
        }).then(res => res, err => {
            console.log(err);  // 输出error
            return Promise.resolve('success');  // 返回一个成功的Promise
        
        }).then(res => {
            console.log(res);
            return 22;  // 返回一个非Promise的值
        
        }).then(res => console.log(res)) // 打印22
        .then(res => console.log(res))   // 打印undefined
```

输出结果如下：

![QQ截图20240515132857](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240515132857.png)

需要注意的是，最后一次打印的`res`是`undefined`，因为上一次的回调函数没有返回值。



## 七、什么是`Promise`的异常穿透？

当使用`Promise`的链式调用时，可以在最后指定失败的回调，当前面操作除了任何异常时，都会传到最后的失败中处理。

如下代码所示：

```js
		const p = Promise.resolve(12);  // p为成功的Promise

        p.then(res => {
            console.log(res);  // 输出12
            return Promise.reject('error');  // 返回一个失败的Promise
        
        }).then(res => {
            console.log(res); 
            return Promise.resolve('success');  // 返回一个成功的Promise
        
        }).catch(err => console.log(err))   // 打印undefined
```

在第一次执行`then`方法时返回了失败的`Promise`对象，之后第三次的`res`输出不再执行，到最后`catch`接到错误，输出`error`。

> 注：若第三次`then`方法中指定了错误情况的回调函数，则会执行该回调，catch中则不会接到错		误对象，除非回调中继续返回错误的Promise对象



八、如何中断`Promise`链？

**只有一种方法：返回未定义状态的`Promise`对象。**因为只有`Promise`的状态改变了，才会执行回调函数。

如下代码所示：

```js
		const p = Promise.resolve(11);

        p.then(res => console.log(res))
         .then(() => console.log(22))
         .then(() => console.log(33))
         .then(() => console.log(44));
```

上述返回结果为：

![QQ截图20240515135217](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240515135217.png)

要想`33`，`44`不打印，则可以在打印`22`的后面返回空的`Promise`对象，如下：

```js
		const p = Promise.resolve(11);

        p.then(res => console.log(res))
         .then(() => {
              console.log(22);
              return new Promise(() => {});
         })
         .then(() => console.log(33))
         .then(() => console.log(44));
```

输出结果如下：

![QQ截图20240515135416](/md-images/学习笔记/Promise.assets/QQ%E6%88%AA%E5%9B%BE20240515135416.png)



# async&await

- `async`一般用在函数上，能够将一个函数的返回结果变为`Promise`对象，对象成功与否的规则与`then`方法完全相同。
- `await`一般用在变量上，可以接收`Promise`返回的**成功的返回值**，若`Promise`对象返回的是失败的值，则需要`try - catch`处理错误
