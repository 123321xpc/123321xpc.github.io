---
title: react18快速入门
published: 2024-06-02
description: ''
image: ''
tags: [学习笔记, react]
category: '学习笔记'
draft: false 
---

- [JSX语法](#jsx语法)
	- [常用JSX语法](#常用jsx语法)
	- [实现列表渲染](#实现列表渲染)
	- [实现基础条件渲染](#实现基础条件渲染)
	- [事件绑定](#事件绑定)
		- [传递自定义参数](#传递自定义参数)
		- [同时传递事件参数和自定义参数](#同时传递事件参数和自定义参数)
- [useState](#usestate)
	- [修改状态的规则](#修改状态的规则)
	- [传递泛型](#传递泛型)
- [组件](#组件)
	- [组件样式](#组件样式)
		- [classnames库](#classnames库)
	- [组件通信](#组件通信)
		- [父传子](#父传子)
			- [children](#children)
		- [子传父](#子传父)
		- [跨层组件](#跨层组件)
- [useEffect](#useeffect)
		- [依赖项](#依赖项)
		- [清除副作用](#清除副作用)
- [hook使用规则](#hook使用规则)
- [Redux](#redux)
	- [配套工具](#配套工具)
	- [store目录结构](#store目录结构)
	- [创建store](#创建store)
	- [注入store](#注入store)
	- [使用store中的数据](#使用store中的数据)
	- [修改store中的数据](#修改store中的数据)
	- [管理异步状态数据](#管理异步状态数据)
- [路由](#路由)
	- [安装](#安装)
	- [路由导航跳转](#路由导航跳转)
	- [声明式导航](#声明式导航)
	- [编程式导航](#编程式导航)
		- [传参](#传参)
	- [嵌套路由](#嵌套路由)
		- [默认二级路由](#默认二级路由)
	- [404路由](#404路由)
	- [2种路由模式](#2种路由模式)
- [useReducer](#usereducer)
- [useMemo](#usememo)
- [React.memo](#reactmemo)
	- [props比较机制](#props比较机制)
- [useCallback](#usecallback)
- [React.forwardRef](#reactforwardref)
- [React.useInperativeHandle](#reactuseinperativehandle)



# JSX语法

![202406031519541](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031519541.png)



- `js表达式`：一个表达式会产生一个值，能放在任何一个需要值的地方
	- 如： `a, a + b, func(1), arr.map`等，凡是能用`const x = `接到值的都是表达式

- `js语句`：`if, for, switch`



## 常用JSX语法

![202406031519905](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031519905.png)



## 实现列表渲染

![202406031519852](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031519852.png)

## 实现基础条件渲染

![202406031520587](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031520587.png)



## 事件绑定

![202406031520992](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031520992.png)



### 传递自定义参数

![202406031520289](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031520289.png)



### 同时传递事件参数和自定义参数

![202406031520435](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031520435.png)



![202406031520102](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/202406031520102.png)

# useState

![image-20240609192018714](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192018714.png)

## 修改状态的规则

![image-20240609192430656](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192430656.png)

![image-20240609192551509](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192551509.png)



## 传递泛型

![image-20240610154311431](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610154311431.png)



![image-20240610154726394](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610154726394.png)







# 组件

## 组件样式

![image-20240609192834816](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609192834816.png)



> 注：
>
> 1. 多个单词必须用小驼峰。
> 2. 是`className`，不是`class`



### classnames库

![image-20240609193706313](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609193706313.png)



## 组件通信

### 父传子

- 父组件传递数据

![image-20240609193952490](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609193952490.png)

- 子组件接收数据

![image-20240609194024452](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194024452.png)

- 说明：

![image-20240609194139934](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194139934.png)

#### children

![image-20240609194601080](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194601080.png)



### 子传父

![image-20240609194709092](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609194709092.png)



### 跨层组件

![image-20240609200105423](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200105423.png)

1. 

![image-20240609195404529](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609195404529.png)

2. 

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609195523677.png" alt="image-20240609195523677" style="zoom:67%;" />

3. 

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609195436584.png" alt="image-20240609195436584" style="zoom: 80%;" />



# useEffect

![image-20240609200801615](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200801615.png)

![image-20240609200439554](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200439554.png)

### 依赖项

![image-20240609200919404](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609200919404.png)

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609201148661.png" alt="image-20240609201148661" style="zoom:50%;" />

>上述代码，每当count改变时，函数就会执行。



### 清除副作用

![image-20240609201324456](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609201324456.png)

 例：

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609201718375.png" alt="image-20240609201718375" style="zoom:50%;" />



# hook使用规则

![image-20240609202538548](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609202538548.png)

# Redux

## 配套工具

![image-20240609203827967](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609203827967.png)

```
pnpm i @reduxjs/toolkit react-redux
```



## store目录结构

![image-20240609204022167](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609204022167.png)

## 创建store

![image-20240609204338761](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609204338761.png)

## 注入store

![image-20240609204750321](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609204750321.png)



## 使用store中的数据

![image-20240609204849056](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609204849056.png)

## 修改store中的数据

![image-20240609205258432](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609205258432.png)

![image-20240609205552395](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609205552395.png)

## 管理异步状态数据

![image-20240609205920758](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240609205920758.png)

> 封装异步函数也写在store文件中。



# 路由

## 安装

```
cnpm i react-router-dom
```



## 路由导航跳转

## 声明式导航

![image-20240610144035333](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144035333.png)

## 编程式导航

![image-20240610144117422](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144117422.png)

### 传参

![image-20240610144554126](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144554126.png)

- 注意：`Param`传参必须要在路由文件中写明键值

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610144935140.png" alt="image-20240610144935140" style="zoom:50%;" />



## 嵌套路由

![image-20240610145100434](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610145100434.png)

### 默认二级路由

![image-20240610145656203](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610145656203.png)

## 404路由

![image-20240610145800181](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610145800181.png)



## 2种路由模式

![image-20240610150024633](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610150024633.png)



# useReducer

![image-20240610150400129](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610150400129.png)



![image-20240610151032828](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151032828.png)

# useMemo

![image-20240610151332204](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151332204.png)



# React.memo

![image-20240610151735143](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151735143.png)

![image-20240610151803008](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610151803008.png)

## props比较机制

![image-20240610152158813](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610152158813.png)

> 当传递的是复杂数据时，比较的是引用是否变化。而当组件重新渲染时，引用会改变！

+ 若需要保证渲染过程中复杂数据的引用不变，可以对数据使用useMemo，如下：

![image-20240610152632237](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610152632237.png)



# useCallback

![image-20240610152802414](https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610152802414.png)

# React.forwardRef

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153235460.png" alt="image-20240610153235460" style="zoom: 33%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153258190.png" alt="image-20240610153258190" style="zoom:33%;" />



# React.useInperativeHandle

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153413782.png" alt="image-20240610153413782" style="zoom:33%;" />

+ 子组件：

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153538540.png" alt="image-20240610153538540" style="zoom:50%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/react快速入门.assets/image-20240610153655032.png" alt="image-20240610153655032" style="zoom:50%;" />
