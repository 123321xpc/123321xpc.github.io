---
title: ES6语法
published: 2024-07-31
description: ''
image: ''
tags: [ES6]
category: '学习笔记'
draft: false 
---





# 变量（const，var，let）

+ **三者区别：**

1. `var`无块级作用域，`let、const`有块级作用域。**（二者均有函数作用域）**

![image-20240731221057667](https://vip.123pan.cn/1828962653/md-images/image-20240731221057667.png)

又如下图：

![image-20240731221539431](https://vip.123pan.cn/1828962653/md-images/image-20240731221539431.png)

+ **上述代码能打印出10，换成`let`则打印不出**

**特别地：**

![image-20240731221935332](https://vip.123pan.cn/1828962653/md-images/image-20240731221935332.png)

+ **上述代码能能访问到`a`，打印`undefined`，因为赋值语句没执行，但是`a`在一开始就定义了。**

2. `var`有变量提升的效果，`let、const`没有。如上图，`var`声明会提升到函数作用域或全局作用域的顶部，但赋值不会提升。这就导致**在声明变量之前可以访问变量**，结果会得到`undefined`（类似于上一张图）

3. `var`可以重复声明，`let、const`不行。如下图所示：

![image-20240731223315855](https://vip.123pan.cn/1828962653/md-images/image-20240731223315855.png)

4. `const`声明变量必须赋值，初始化。

![image-20240731223730085](https://vip.123pan.cn/1828962653/md-images/image-20240731223730085.png)



# 解构赋值

```typescript
// 解构数组
const arr = ['hello', 'world', 'leetcode']
const [a, b, c] = arr
console.log('a: ',a, 'b: ',b, 'c: ',c)

// 解构对象
const obj = {age: 26, city: 'Beijing'}
const {age, city} = obj
console.log('age: ',age, 'city: ',city)
```

![image-20240731224614222](https://vip.123pan.cn/1828962653/md-images/image-20240731224614222.png)

+ 利用解构赋值交换2个数：

```typescript
let a = 1;
let b = 2;
[a, b] = [b, a];	// 结果为a = 2, b = 1
```



## 底层原理

1. 对于数组解构赋值，JavaScript 引擎会迭代目标数组的每一个元素，并根据解构模式将值分配给相应的变量。例如：

```
let [a, b, c] = [1, 2, 3];
```

底层会进行类似于以下步骤的操作：

1. 创建一个迭代器来遍历数组 `[1, 2, 3]`。
2. 取出第一个值 `1`，并将其赋值给变量 `a`。
3. 取出第二个值 `2`，并将其赋值给变量 `b`。
4. 取出第三个值 `3`，并将其赋值给变量 `c`。



2. 对于对象解构赋值，JavaScript 引擎会根据解构模式中的属性名来查找目标对象中的对应属性。例如：

```
let {x, y} = {x: 1, y: 2};
```

底层会进行类似于以下步骤的操作：

1. 查找对象 `{x: 1, y: 2}` 中名为 `x` 的属性，并将其值 `1` 赋值给变量 `x`。
2. 查找对象 `{x: 1, y: 2}` 中名为 `y` 的属性，并将其值 `2` 赋值给变量 `y`。



3. 对于嵌套解构赋值，JavaScript 引擎会递归地应用解构赋值规则。例如：

```
let {a: {b, c}} = {a: {b: 1, c: 2}};
```

底层会进行类似于以下步骤的操作：

1. 查找对象 `{a: {b: 1, c: 2}}` 中名为 `a` 的属性，其值为 `{b: 1, c: 2}`。
2. 对 `{b: 1, c: 2}` 进行解构，将 `b` 的值 `1` 赋值给变量 `b`，将 `c` 的值 `2` 赋值给变量 `c`。



**4. Symbol.iterator**

对于数组解构赋值，底层实现依赖于目标对象的 `Symbol.iterator` 方法来进行迭代。如果目标对象没有实现迭代器协议，则解构赋值会失败。



# 展开运算符

```typescript
const sum = (a, b, c) => a + b + c;
const arr = [1, 2, 3];

const res = sum(...arr); // qian
console.log(res); // 6
```



## 底层实现

1. 调用 `arr[Symbol.iterator]()` 方法获取迭代器对象。
2. 使用迭代器对象逐一获取每个值，直到迭代器的 `done` 属性为 `true`。
3. 将这些值按顺序插入到新的数组中。
4. 在新数组末尾追加 `4` 和 `5`。



# 箭头函数特点

1. ## 无`arguments`数组：

![image-20240801221152341](https://vip.123pan.cn/1828962653/md-images/image-20240801221152341.png)

+ **原因：`arguments`是类数组对象，无法使用数组方法操作。**
+ **之后引入`args`剩余参数对象，这个是数组，可以使用所有数组方法****，同时可以配合其他参数使用，如下：**

```js
const fn2 = (a, b, ...args) => {
    console.log(args);
    
}

fn2(1, 2, 3, 4);	// 结果：[3, 4]
```



## 2. 箭头函数没有this

+ 如果在箭头函数中使用`this`，会自动寻找最近的外层作用域的`this`，如下：

```js
const fn = () => {
     console.log(this);
}

fn();
```

+ 结果：

![image-20240801222743246](https://vip.123pan.cn/1828962653/md-images/image-20240801222743246.png)



![image-20240801223846663](https://vip.123pan.cn/1828962653/md-images/image-20240801223846663.png)

+ 结果：`undefined`
+ 原因：
	+ 由于箭头函数 `f` 捕获了 `fn` 调用时的 `this`，而 `fn` 调用时的 `this` 是全局对象。因此，`this.a` 实际上是全局对象 `a` 的值。
	+ 在全局对象中，没有一个名为 `a` 的属性（**因为全局变量 `a` 是通过 `let` 声明的，它不会成为全局对象的属性**）。因此，`this.a` 的值是 `undefined`。
	+ **如果是`var`，定义的变量，则会变成对象的属性**，如下图：

![image-20240801224428626](https://vip.123pan.cn/1828962653/md-images/image-20240801224428626.png)

+ 打印结果为：200

![image-20240801224628372](https://vip.123pan.cn/1828962653/md-images/image-20240801224628372.png)

+ 打印结果为：200

![image-20240801224712835](https://vip.123pan.cn/1828962653/md-images/image-20240801224712835.png)

+ 打印结果为：100**（`var`有函数作用域）**



## 3. 箭头函数无法作为构造函数使用

+ 即不能使用`new`创建对象



# 模块化

+ 默认导出：**（一个模块只能有一个默认导出）**

```js
const a = 100;
const b = 200

export default a;
```

+ 选择导出

```js
export const c = 300;
```

+ 默认导入：

```js
import haha from a.js	// 导入后为默认导出的值（a）

console.log(haha)	// 输出100
```

+ 选择导入：

```
import {c as d} from a.js

console.log(d)	// 输出300
```



# 数组方法

## map：根据数组返回新数组

+ **不破坏原数组**
+ 回调函数的参数：
	1. `item`：当前元素
	2. `index`：索引
	3. `arr`：当前数组

![image-20240801230711644](https://vip.123pan.cn/1828962653/md-images/image-20240801230711644.png)

![image-20240801231012645](https://vip.123pan.cn/1828962653/md-images/image-20240801231012645.png)



## filter：过滤，筛选合适的数

+ 根据回调函数结果判断是否保留该数。
+ **不破坏原数组**
+ 回调函数的参数：
	1. `item`：当前元素
	2. `index`：索引
	3. `arr`：当前数组

![image-20240801231227645](https://vip.123pan.cn/1828962653/md-images/image-20240801231227645.png)



## reduce：合并数组中的元素

+ 参数

	1. 回调函数

		+ `preVal`：前一个元素

		+ `currVal`：当前元素

	2. 初始值：指定第一次计算时`pre`的值，若不指定，则直接从第二次计算开始

![image-20240801231714128](https://vip.123pan.cn/1828962653/md-images/image-20240801231714128.png)

+ 结果：

![image-20240801231724690](https://vip.123pan.cn/1828962653/md-images/image-20240801231724690.png)
