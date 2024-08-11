---
title: vue 学习笔记
published: 2024-05-30
description: ''
image: ''
tags: [vue, 学习笔记]
category: '学习笔记'
draft: false 
---

- [安装淘宝镜像cnpm](#安装淘宝镜像cnpm)
- [json-server](#json-server)
  - [安装](#安装)
  - [配置](#配置)
  - [启动](#启动)
- [pm2项目部署托管](#pm2项目部署托管)
  - [部署项目](#部署项目)
  - [查看项目列表](#查看项目列表)
- [vue2语法](#vue2语法)
  - [数据代理](#数据代理)
    - [Object.defineProperty](#objectdefineproperty)
    - [Vue中的数据代理](#vue中的数据代理)
  - [事件](#事件)
    - [$event参数](#event参数)
    - [事件修饰符](#事件修饰符)
    - [键盘事件](#键盘事件)
  - [计算属性computed](#计算属性computed)
    - [简写](#简写)
  - [监视属性watch](#监视属性watch)
    - [深度监视](#深度监视)
    - [简写](#简写-1)
    - [与computed比较](#与computed比较)
  - [样式绑定](#样式绑定)
  - [条件渲染v-if / v-show](#条件渲染v-if--v-show)
  - [列表渲染v-for](#列表渲染v-for)
    - [key内部对比算法](#key内部对比算法)
    - [例子：实现搜索关键字进行列表筛选](#例子实现搜索关键字进行列表筛选)
      - [watch实现](#watch实现)
      - [computed实现](#computed实现)
  - [Vue如何监测数据改变](#vue如何监测数据改变)
  - [过滤器filters](#过滤器filters)
  - [内置指令](#内置指令)
    - [v-cloak](#v-cloak)
    - [v-once](#v-once)
    - [v-pre](#v-pre)
  - [组件传参](#组件传参)
    - [父传子props](#父传子props)
  - [混合mixin](#混合mixin)
  - [插件plugins](#插件plugins)
  - [样式范围scoped](#样式范围scoped)
  - [全局事件总线bus](#全局事件总线bus)
  - [消息订阅和发布pubsub-js](#消息订阅和发布pubsub-js)
  - [$nextTick](#nexttick)
  - [Vue动画](#vue动画)
  - [插槽slot](#插槽slot)
    - [默认插槽：](#默认插槽)
    - [具名插槽：](#具名插槽)
    - [作用域插槽：](#作用域插槽)
  - [Vuex](#vuex)
    - [搭建vuex环境](#搭建vuex环境)
    - [基本使用](#基本使用)
    - [getters的使用（vuex中的计算属性）](#getters的使用vuex中的计算属性)
    - [四个map方法的使用](#四个map方法的使用)
    - [模块化+命名空间](#模块化命名空间)
  - [路由](#路由)
    - [基本使用](#基本使用-1)
    - [几个注意点](#几个注意点)
    - [多级路由（多级路由）](#多级路由多级路由)
    - [路由的query参数](#路由的query参数)
    - [命名路由](#命名路由)
    - [路由的params参数](#路由的params参数)
    - [路由的props配置](#路由的props配置)
    - [```<router-link>```的replace属性](#router-link的replace属性)
    - [编程式路由导航](#编程式路由导航)
    - [缓存路由组件](#缓存路由组件)
    - [两个新的生命周期钩子](#两个新的生命周期钩子)
    - [路由守卫](#路由守卫)
    - [路由器的两种工作模式](#路由器的两种工作模式)
- [Vue生命周期](#vue生命周期)
- [其他](#其他)
  - [CSS全局变量](#css全局变量)
  - [本地缓存storage](#本地缓存storage)
  - [使用在线连接导入自定义图标库](#使用在线连接导入自定义图标库)
- [创建工程(Vue2)](#创建工程vue2)
  - [安装less](#安装less)
  - [安装脚手架](#安装脚手架)
  - [关闭eslint报错](#关闭eslint报错)
  - [为什么需要render函数](#为什么需要render函数)
  - [main.ts初始代码](#maints初始代码)
  - [vite.config.ts初始代码](#viteconfigts初始代码)
  - [配置全局用户代码片段](#配置全局用户代码片段)
  - [开发多页面](#开发多页面)
  - [配置代理](#配置代理)
    - [方法一](#方法一)
    - [方法二](#方法二)
  - [导入包](#导入包)
    - [自动生成唯一id包](#自动生成唯一id包)
    - [echarts](#echarts)
    - [axios](#axios)
    - [element](#element)
      - [插件导入中文包](#插件导入中文包)
      - [按需引入](#按需引入)
    - [element-plus](#element-plus)
- [使用vite创建工程(Vue3)](#使用vite创建工程vue3)
  - [配置开发环境和生产环境](#配置开发环境和生产环境)
  - [浏览器自动打开](#浏览器自动打开)
  - [安装Vite-setup插件](#安装vite-setup插件)
  - [安装TypeScript Vue Plugin](#安装typescript-vue-plugin)
  - [自动本地持久化](#自动本地持久化)
  - [仓库的统一管理](#仓库的统一管理)
  - [组件自动注册](#组件自动注册)
  - [全局组件类型自动识别](#全局组件类型自动识别)
  - [打包svg地图](#打包svg地图)
  - [svg组件封装](#svg组件封装)
  - [修改加载进度条](#修改加载进度条)
  - [移动端适配](#移动端适配)
    - [获取设备宽度](#获取设备宽度)
- [Vue3语法](#vue3语法)
  - [Omit](#omit)
  - [定义响应式数据](#定义响应式数据)
  - [toRefs](#torefs)
  - [computed](#computed)
  - [watch](#watch)
    - [解除监视](#解除监视)
    - [监视ref定义的对象类型](#监视ref定义的对象类型)
    - [监视reactive定义的对象类型](#监视reactive定义的对象类型)
    - [监视对象的某个属性](#监视对象的某个属性)
    - [监视多个数据](#监视多个数据)
  - [watchEffect](#watcheffect)
  - [ref代替id打标识](#ref代替id打标识)
  - [定义接口，自定义类型](#定义接口自定义类型)
  - [hooks](#hooks)
  - [路由](#路由-1)
    - [meta.env.BASE\_URL](#metaenvbase_url)
    - [嵌套路由](#嵌套路由)
    - [路由传参](#路由传参)
    - [props](#props)
    - [编程式导航](#编程式导航)
    - [重定向](#重定向)
    - [路由守卫](#路由守卫-1)
  - [slot插槽](#slot插槽)
    - [默认插槽](#默认插槽-1)
    - [具名插槽](#具名插槽-1)
    - [作用域插槽](#作用域插槽-1)
  - [toRaw](#toraw)
  - [subspense](#subspense)
  - [组件通信](#组件通信)
    - [props（父传子）](#props父传子)
    - [custon-event自定义事件（子传父）](#custon-event自定义事件子传父)
    - [mitt（任意组件传值）](#mitt任意组件传值)
    - [$attrs（祖孙通信）](#attrs祖孙通信)
    - [$refs](#refs)
    - [$parent](#parent)
    - [provide](#provide)
- [pinia](#pinia)
  - [读数据](#读数据)
  - [修改数据](#修改数据)
  - [计算属性：getters](#计算属性getters)
  - [监视器：$subscribe](#监视器subscribe)
- [less](#less)
  - [运算](#运算)
  - [变量](#变量)
  - [导入](#导入)
  - [导出](#导出)
  - [禁止导出](#禁止导出)
- [技巧](#技巧)
  - [全选和取消全选使用计算属性](#全选和取消全选使用计算属性)
  - [实现上方导航条(移动端)](#实现上方导航条移动端)
  - [自定义单选按钮组件封装](#自定义单选按钮组件封装)
  - [showConfirmDialog](#showconfirmdialog)
  - [获取自定义类型中的所有类型](#获取自定义类型中的所有类型)




# 安装淘宝镜像cnpm

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```



# json-server

## 安装

```
cnpm i json-server -g
```



## 配置

在根目录创建文件 `db.json` :

```json
{
  "posts": [
    { "id": "1", "title": "a title", "views": 100 },
    { "id": "2", "title": "another title", "views": 200 }
  ],
  "comments": [
    { "id": "1", "text": "a comment about post 1", "postId": "1" },
    { "id": "2", "text": "another comment about post 1", "postId": "1" }
  ],
  "profile": {
    "name": "typicode"
  }
}
```



## 启动

```
json-server --watch db.json
```



# pm2项目部署托管

```
cnpm i pm2 -g
```



## 部署项目

**注：如果项目使用history路由模式，需要配置SPA单页面模式！**

- 首先进入项目文件夹

- 然后

	- ```
		pm2 serve ./ 8080 --name myproject
		```

	- ```
		pm2 serve --spa ./ 8080 --name myproject
		```

	- 



## 查看项目列表

```
pm2 list
```









# vue2语法

## 数据代理

### Object.defineProperty

- 可以往json中添加属性
- 添加的属性具有特殊性质：
	- 无法遍历，枚举，修改，删除
	- 有get，set方法

![QQ截图20240323210057](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240323210057.png)



### Vue中的数据代理

![QQ截图20240323211518](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240323211518.png)

![QQ截图20240323211507](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240323211507.png)



## 事件

### $event参数

![QQ截图20240323212535](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240323212535.png)





### 事件修饰符

![QQ截图20240323212732](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240323212732.png)

- 注：修饰符可以连写。如`@click.prevent.stop`



### 键盘事件

![QQ截图20240325152830](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325152830.png)





## 计算属性computed

![QQ截图20240325155514](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325155514.png) 

+ 例：

![QQ截图20240325155534](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325155534.png)



### 简写

![QQ截图20240325155912](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325155912.png)



## 监视属性watch

![QQ截图20240325160449](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325160449.png)

![QQ截图20240325160519](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325160519.png)

### 深度监视

![QQ截图20240325161051](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325161051.png)

![QQ截图20240325161152](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325161152.png)



### 简写

![QQ截图20240325161508](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325161508.png)

![QQ截图20240325161453](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325161453.png)



### 与computed比较

![QQ截图20240325162445](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325162445.png)



## 样式绑定

![QQ截图20240325165023](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325165023.png)

![QQ截图20240325165118](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240325165118.png)



## 条件渲染v-if / v-show

![QQ截图20240328185859](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240328185859.png)



## 列表渲染v-for

### key内部对比算法

![QQ截图20240328193355](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240328193355.png)



### 例子：实现搜索关键字进行列表筛选

#### watch实现

![QQ截图20240328200218](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240328200218-17116273558231.png)

- 注：
	1. `filPersons`用于展示搜索后的列表。
	2. `watch`中的`immediate`属性用于一开始自动搜索一次空字符串，从而一开始显示所有数据。因为`indexOf`方法中默认所有字符串都包含空字符串。



#### computed实现

![QQ截图20240328200921](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240328200921.png)



- 扩展：筛选 + 排序

![QQ截图20240328201610](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240328201610.png)



## Vue如何监测数据改变 

![QQ截图20240328210743](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240328210743.png)

 

## 过滤器filters

![QQ截图20240330133644](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330133644.png)

![QQ截图20240330132927](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330132927.png)

![QQ截图20240330132945](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330132945.png)

- **过滤器可传参，可串联**



## 内置指令

### v-cloak

![QQ截图20240330140004](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330140004.png)



### v-once

![QQ截图20240330140145](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330140145.png)



### v-pre

![QQ截图20240330140339](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330140339.png)





## 组件传参

### 父传子props

- 父组件：

![QQ截图20240330190207](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330190207.png)

- 子组件

![QQ截图20240330190337](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330190337.png)

- 最完整写法

![QQ截图20240330190458](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330190458.png)

注意：

![QQ截图20240330191004](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330191004.png)



## 混合mixin

![QQ截图20240330191648](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330191648.png)

- mixin.js：

![QQ截图20240330191744](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330191744.png)

![QQ截图20240330191840](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330191840.png)



## 插件plugins

![QQ截图20240330192634](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330192634.png)

- plugins.js：

![QQ截图20240330192716](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330192716.png)

- 使用：`main.js`中：`Vue.use(plugins)`



## 样式范围scoped

- 本质：在标签上加上标识，然后配合范围选择器

![QQ截图20240330193140](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330193140.png)

 

## 全局事件总线bus

- 安装

![QQ截图20240401204630](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401204630.png)

- 使用和删除

![QQ截图20240401204941](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401204941.png)



## 消息订阅和发布pubsub-js

+ 安装

```
cnpm i pub
```



- 引入库：

![QQ截图20240401205746](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401205746.png)

- 订阅消息（接收消息）：

![QQ截图20240401210608](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401210608.png)

- 发布消息：

![QQ截图20240401210321](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401210321.png)

- 取消订阅：

![QQ截图20240401210615](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401210615.png)



## $nextTick

![QQ截图20240401210923](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401210923.png)



## Vue动画

<img src="https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401213236.png" alt="QQ截图20240401213236" style="z" />

- 例：

![QQ截图20240401212253](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401212253.png)



- 若显示动画和隐藏动画互为反转：

![QQ截图20240401212358](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401212358.png)

- 多个元素过度

![QQ截图20240401212815](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401212815.png)

- 第三方动画库`Animate.css`
	- 引入：`import animate.css`
	- 使用：

![QQ截图20240401213116](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240401213116.png)



## 插槽slot

### 默认插槽：

```vue
父组件中：
        <Category>
           <div>html结构1</div>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot>插槽默认内容...</slot>
            </div>
        </template>
```

### 具名插槽：

```vue
父组件中：
        <Category>
            <template slot="center">
              <div>html结构1</div>
            </template>

            <template v-slot:footer>
               <div>html结构2</div>
            </template>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot name="center">插槽默认内容...</slot>
               <slot name="footer">插槽默认内容...</slot>
            </div>
        </template>
```

###  作用域插槽：

1. 理解：<span style="color:red">数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。</span>（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）

2. 具体编码：

	```vue
	父组件中：
			<Category>
				<template scope="scopeData">
					<!-- 生成的是ul列表 -->
					<ul>
						<li v-for="g in scopeData.games" :key="g">{{g}}</li>
					</ul>
				</template>
			</Category>
	
			<Category>
				<template slot-scope="scopeData">
					<!-- 生成的是h4标题 -->
					<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
				</template>
			</Category>
	子组件中：
	        <template>
	            <div>
	                <slot :games="games"></slot>
	            </div>
	        </template>
			
	        <script>
	            export default {
	                name:'Category',
	                props:['title'],
	                //数据在子组件自身
	                data() {
	                    return {
	                        games:['红色警戒','穿越火线','劲舞团','超级玛丽']
	                    }
	                },
	            }
	        </script>
	```



## Vuex

### 搭建vuex环境

创建文件：```src/store/index.js```

```js
//引入Vue核心库
import Vue from 'vue'
//引入Vuex
import Vuex from 'vuex'
//应用Vuex插件
Vue.use(Vuex)

//准备actions对象——响应组件中用户的动作
const actions = {}
//准备mutations对象——修改state中的数据
const mutations = {}
//准备state对象——保存具体的数据
const state = {}

//创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state
})
```

在```main.js```中创建vm时传入```store```配置项

```js
......
//引入store
import store from './store'
......

//创建vm
new Vue({
	el:'#app',
	render: h => h(App),
	store
})
```

###    基本使用

初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

```js
//引入Vue核心库
import Vue from 'vue'
//引入Vuex
import Vuex from 'vuex'
//引用Vuex
Vue.use(Vuex)

const actions = {
    //响应组件中加的动作
	jia(context,value){
		// console.log('actions中的jia被调用了',miniStore,value)
		context.commit('JIA',value)
	},
}

const mutations = {
    //执行加
	JIA(state,value){
		// console.log('mutations中的JIA被调用了',state,value)
		state.sum += value
	}
}

//初始化数据
const state = {
   sum:0
}

//创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state,
})
```

1. 组件中读取vuex中的数据：```$store.state.sum```

2. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)``` 或 ```$store.commit('mutations中的方法名',数据)```

	>  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```

### getters的使用（vuex中的计算属性）

概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。

在```store.js```中追加```getters```配置

```js
......

const getters = {
	bigSum(state){
		return state.sum * 10
	}
}

//创建并暴露store
export default new Vuex.Store({
	......
	getters
})
```

组件中读取数据：```$store.getters.bigSum```

### 四个map方法的使用

<strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性

```js
computed: {
    //借助mapState生成计算属性：sum、school、subject（对象写法）
     ...mapState({sum:'sum',school:'school',subject:'subject'}),
         
    //借助mapState生成计算属性：sum、school、subject（数组写法）
    ...mapState(['sum','school','subject']),
},
```

<strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

```js
computed: {
    //借助mapGetters生成计算属性：bigSum（对象写法）
    ...mapGetters({bigSum:'bigSum'}),

    //借助mapGetters生成计算属性：bigSum（数组写法）
    ...mapGetters(['bigSum'])
},
```

<strong>mapActions方法：</strong>用于帮助我们生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数

```js
methods:{
    //靠mapActions生成：incrementOdd、incrementWait（对象形式）
    ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})

    //靠mapActions生成：incrementOdd、incrementWait（数组形式）
    ...mapActions(['jiaOdd','jiaWait'])
}
```

<strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

```js
methods:{
    //靠mapActions生成：increment、decrement（对象形式）
    ...mapMutations({increment:'JIA',decrement:'JIAN'}),
    
    //靠mapMutations生成：JIA、JIAN（对象形式）
    ...mapMutations(['JIA','JIAN']),
}
```

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，如`@click=increat(value1, value2)`，否则参数是事件对象。

### 模块化+命名空间

目的：让代码更好维护，让多种数据分类更加明确。

修改```store.js```

```javascript
const countAbout = {
  namespaced:true,//开启命名空间
  state:{x:1},
  mutations: { ... },
  actions: { ... },
  getters: {
    bigSum(state){
       return state.sum * 10
    }
  }
}

const personAbout = {
  namespaced:true,//开启命名空间
  state:{ ... },
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    countAbout,
    personAbout
  }
})
```

开启命名空间后，组件中读取state数据：

```js
//方式一：自己直接读取
this.$store.state.personAbout.list
//方式二：借助mapState读取：
...mapState('countAbout',['sum','school','subject']),
```

开启命名空间后，组件中读取getters数据：

```js
//方式一：自己直接读取
this.$store.getters['personAbout/firstPersonName']
//方式二：借助mapGetters读取：
...mapGetters('countAbout',['bigSum'])
```

开启命名空间后，组件中调用dispatch

```js
//方式一：自己直接dispatch
this.$store.dispatch('personAbout/addPersonWang',person)
//方式二：借助mapActions：
...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
```

开启命名空间后，组件中调用commit

```js
//方式一：自己直接commit
this.$store.commit('personAbout/ADD_PERSON',person)
//方式二：借助mapMutations：
...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
```



 ## 路由

1. 理解： 一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。
2. 前端路由：key是路径，value是组件。

### 基本使用

1. 安装vue-router，命令：```npm i vue-router```

2. 应用插件：```Vue.use(VueRouter)```

3. 编写router配置项:

	```js
	//引入VueRouter
	import VueRouter from 'vue-router'
	//引入Luyou 组件
	import About from '../components/About'
	import Home from '../components/Home'
	
	//创建router实例对象，去管理一组一组的路由规则
	const router = new VueRouter({
		routes:[
			{
				path:'/about',
				component:About
			},
			{
				path:'/home',
				component:Home
			}
		]
	})
	
	//暴露router
	export default router
	```

4. 实现切换（active-class可配置高亮样式）

	```vue
	<router-link active-class="active" to="/about">About</router-link>
	```

5. 指定展示位置

	```vue
	<router-view></router-view>
	```

### 几个注意点

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在```components```文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到。

### 多级路由（多级路由）

1. 配置路由规则，使用children配置项：

	```js
	routes:[
		{
			path:'/about',
			component:About,
		},
		{
			path:'/home',
			component:Home,
			children:[ //通过children配置子级路由
				{
					path:'news', //此处一定不要写：/news
					component:News
				},
				{
					path:'message',//此处一定不要写：/message
					component:Message
				}
			]
		}
	]
	```

2. 跳转（要写完整路径）：

	```vue
	<router-link to="/home/news">News</router-link>
	```

### 路由的query参数

1. 传递参数

	```vue
	<!-- 跳转并携带query参数，to的字符串写法 -->
	<router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>
					
	<!-- 跳转并携带query参数，to的对象写法 -->
	<router-link 
		:to="{
			path:'/home/message/detail',
			query:{
			   id:666,
	            title:'你好'
			}
		}"
	>跳转</router-link>
	```

2. 接收参数：

	```js
	$route.query.id
	$route.query.title
	```

### 命名路由

作用：可以简化路由的跳转。

给路由命名：

```js
{
	path:'/demo',
	component:Demo,
	children:[
		{
			path:'test',
			component:Test,
			children:[
				{
                      name:'hello' //给路由命名
					path:'welcome',
					component:Hello,
				}
			]
		}
	]
}
```

简化跳转：

```vue
<!--简化前，需要写完整的路径 -->
<router-link to="/demo/test/welcome">跳转</router-link>

<!--简化后，直接通过名字跳转 -->
<router-link :to="{name:'hello'}">跳转</router-link>

<!--简化写法配合传递参数 -->
<router-link 
	:to="{
		name:'hello',
		query:{
		   id:666,
            title:'你好'
		}
	}"
>跳转</router-link>
```

### 路由的params参数

1. 配置路由，声明接收params参数

	```js
	{
		path:'/home',
		component:Home,
		children:[
			{
				path:'news',
				component:News
			},
			{
				component:Message,
				children:[
					{
						name:'xiangqing',
						path:'detail/:id/:title', //使用占位符声明接收params参数
						component:Detail
					}
				]
			}
		]
	}
	```

2. 传递参数

	```vue
	<!-- 跳转并携带params参数，to的字符串写法 -->
	<router-link :to="/home/message/detail/666/你好">跳转</router-link>
					
	<!-- 跳转并携带params参数，to的对象写法 -->
	<router-link 
		:to="{
			name:'xiangqing',
			params:{
			   id:666,
	            title:'你好'
			}
		}"
	>跳转</router-link>
	```

	> 特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！

3. 接收参数：

	```js
	$route.params.id
	$route.params.title
	```

### 路由的props配置

​	作用：让路由组件更方便的收到参数

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props(route){
		return {
			id:route.query.id,
			title:route.query.title
		}
	}
}
```

### ```<router-link>```的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为```push```和```replace```，```push```是追加历史记录，```replace```是替换当前记录。路由跳转时候默认为```push```
3. 如何开启```replace```模式：```<router-link replace .......>News</router-link>```

### 编程式路由导航

作用：不借助```<router-link> ```实现路由跳转，让路由跳转更加灵活

具体编码：

```js
//$router的两个API
this.$router.push({
	name:'xiangqing',
		params:{
			id:xxx,
			title:xxx
		}
})

this.$router.replace({
	name:'xiangqing',
		params:{
			id:xxx,
			title:xxx
		}
})
this.$router.forward() //前进
this.$router.back() //后退
this.$router.go() //可前进也可后退
```

### 缓存路由组件

作用：让不展示的路由组件保持挂载，不被销毁。

具体编码：

```vue
<keep-alive include="News"> 
    <router-view></router-view>
</keep-alive>
```

### 两个新的生命周期钩子

作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。

具体名字：

1. ```activated```路由组件被激活时触发。
2. ```deactivated```路由组件失活时触发。

### 路由守卫

作用：对路由进行权限控制

分类：全局守卫、独享守卫、组件内守卫

全局守卫:

```js
//全局前置守卫：初始化时执行、每次路由切换前执行
router.beforeEach((to,from,next)=>{
	console.log('beforeEach',to,from)
	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
			next() //放行
		}else{
			alert('暂无权限查看')
			// next({name:'guanyu'})
		}
	}else{
		next() //放行
	}
})

//全局后置守卫：初始化时执行、每次路由切换后执行
router.afterEach((to,from)=>{
	console.log('afterEach',to,from)
	if(to.meta.title){ 
		document.title = to.meta.title //修改网页的title
	}else{
		document.title = 'vue_test'
	}
})
```

独享守卫:

```js
beforeEnter(to,from,next){
	console.log('beforeEnter',to,from)
	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'atguigu'){
			next()
		}else{
			alert('暂无权限查看')
			// next({name:'guanyu'})
		}
	}else{
		next()
	}
}
```

组件内守卫：

```js
//进入守卫：通过路由规则，进入该组件时被调用
beforeRouteEnter (to, from, next) {
},
//离开守卫：通过路由规则，离开该组件时被调用
beforeRouteLeave (to, from, next) {
}
```

### 路由器的两种工作模式



1. 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。

2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。

3. hash模式：

	1. 地址中永远带着#号，不美观 。
	2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
	3. 兼容性较好。

4. history模式：

	1. 地址干净，美观 。
	2. 兼容性和hash模式相比略差。
	3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

	 







# Vue生命周期

![生命周期](https://vip.123pan.cn/1828962653/md-images/vue.assets/生命周期.png)





# 其他

## CSS全局变量

<img src="https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240424160623.png" alt="QQ截图20240424160623" style="zoom:50%;" />



## 本地缓存storage

![QQ截图20240330210851](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330210851.png)



## 使用在线连接导入自定义图标库

- 要在生成的链接前加上`https:`
- 例如：`    @import 'https://at.alicdn.com/t/c/font_4519967_pfb00em8bza.css';`





# 创建工程(Vue2)

```
vue create app
```





## 安装less

```
cnpm add less-loader less
```





## 安装脚手架

```
cnpm i @vue/cli -g    
```



## 关闭eslint报错

```js
module.exports = defineConfig({
  transpileDependencies: true,
  lintOnSave: false
})
```



## 为什么需要render函数

![QQ截图20240330183408](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330183408.png)





## main.ts初始代码

```js
import './assets/main.css'
import { createApp } from 'vue'
import App from './App.vue'
const app = createApp(App)

//router
import router from './router'
app.use(router)

//pinia
import { createPinia } from "pinia"
const pinia = createPinia()
app.use(pinia)

//mitt
import emitter from './utils/emitter'

app.mount('#app')
```



## vite.config.ts初始代码

```js
import { fileURLToPath, URL } from 'node:url'
import vuesetup from "vite-plugin-vue-setup-extend";
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    vuesetup(),
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    })
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  }
})

```





## 配置全局用户代码片段

```json
{
	"axios.pose": {
		"prefix": "myaxios.pose",
		"body": [
			"try {"                                          
			"	const {data:res} = await this.\\$axios({"
			"		method: 'post',"
			"		url: '/api/tickets/changedate',"
			"		data: "
			"	})"

			"	if(res.code === 200)"
			"	{"

			"	}"
			"	else this.msg(res.msg, res.data)"
            "} catch (error) {this.msg()}"
            
		],
		"description": "axios"
	},
	"axios.get": {
		"prefix": "myaxios.get",
		"body": [
			"try {"                                          
			"	const {data:res} = await this.\\$axios({"
			"		method: 'get',"
			"		url: '/api',"
			"	})"

			"	if(res.code === 200)"
			"	{"

			"	}"
			"	else this.msg(res.msg, res.data)"
            "} catch (error) {error.message; this.msg()}"
            
		],
		"description": "axios"
	}

},
```





## 开发多页面

```js
module.exports = defineConfig({
  publicPath:process.env.NODE_ENV==='production'?'./':'/',
  pages:{
    login:{
      entry:'src/pages/login/login.js',   //页面js
      template: 'public/login.html',      //页面输出文件html
      filename: 'login.html',             //文件名
      title: 'Login Page',                //标题
      chunks: ['chunk-vendors', 'chunk-common', 'login']  //前两个属性固定，后一个为该页面的名字
    },
      index:{
          entry:'src/pages/index/index.js',
          template: 'public/index.html',
          filename: 'index.html',		//必须要有一个页面输出路径为index.html，且该页面为默认
          title: 'Index Page',
          chunks: ['chunk-vendors', 'chunk-common', 'index']
      }
  }
})
```



## 配置代理

### 方法一

​	在vue.config.js中添加如下配置：

```js
devServer:{
  proxy:"http://localhost:5000"
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源）

### 方法二

​	编写vue.config.js配置具体代理规则：

```js
module.exports = {
	devServer: {
      proxy: {
      '/api1': {// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api1': ''}
      },
      '/api2': {// 匹配所有以 '/api2'开头的请求路径
        target: 'http://localhost:5001',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api2': ''}
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理。
2. 缺点：配置略微繁琐，请求资源时必须加前缀。



## 导入包

### 自动生成唯一id包

```js
cnpm i nanoid

//使用

let a = {id: nanoid()}
```



### echarts

- 注：一定要导入4+版本的

```
cnpm add echarts@4 -S
```

+ 使用

```js
<template>
    <div id="main" style="width: 1000px;height:800px;"></div>
</template>

import * as echarts from 'echarts';
import "echarts/map/js/china.js";

var option = {
    ......
}

export default {
            mounted(){
                var myChart = echarts.init(document.getElementById('main'));
                myChart.setOption(option)
            }
        }
```



### axios

+ `axios.ts:`（移动端，vant）

```js
import axios, { AxiosError, type Method } from 'axios';
import {useUserStore} from'../stores/index';
import { showToast } from 'vant';
import router from '../router';

const instance = axios.create({
  baseURL: 'https://consult-api.itheima.net/',
  timeout: 10000
});

instance.interceptors.request.use(
  (config) => {
    // 处理token
    const store = useUserStore();
    if (store.user?.token && config.headers) {
      config.headers.Authorization = `Bearer ${store.user.token}`;
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  },
);

instance.interceptors.response.use(
    (res) => {
      // 处理访问错误情况
      if(res.data.code !== 10000){
        // 弹出提示(移动端)
        showToast(res.data.message || '请求失败');
        return Promise.reject(res.data);
      }
      return res.data;
    },
    (error : AxiosError) => {
      // 处理token失效401
      if (error.response?.status === 401) {
        // 清除本地用户登录信息
        const store = useUserStore();
        store.delUser();
        // 跳转到登录页面
        router.push({
          path: '/login',
          query: {
            returnUrl: router.currentRoute.value.fullPath
          }
        })
      }
      return Promise.reject(error);
    },
)

// 定义接口返回数据类型
type Data<T> = {
  code: number;
  message: string;
  data: T;
}

// 封装请求方法
export const request = <T>(url: string, method: Method = 'GET', data?: object) => {
     return instance.request<any, Data<T>>({
       url,
       method,
       // 动态属性
       [method.toUpperCase() === 'GET'? 'params' : 'data'] : data
     }) 
}
```



+ `axios.ts`：（H5端，element-plus）

```js
import axios, { AxiosError, type Method } from 'axios';
import { ElMessage } from 'element-plus';

const instance = axios.create({
  baseURL: 'https://localhost:8080/',
  timeout: 10000
});

instance.interceptors.request.use(
  (config) => {
    return config;
  },
  (error) => {
    ElMessage({
        message: '请求失败，请稍后再试！',
        type: 'error'
    })
    return Promise.reject(error);
  },
);

instance.interceptors.response.use(
    (res) => {
        if(res.data.code !== 200){
            ElMessage({
                message: '请求失败，请稍后再试！',
                type: 'error'
            })
        }
        
      return res.data;
    },
    (error : AxiosError) => {
        ElMessage({
            message: '请求失败，请稍后再试！',
            type: 'error'
        })
      return Promise.reject(error);
    },
)

// 定义接口返回数据类型
type Data<T> = {
  code: number;
  message: string;
  data: T;
}

// 封装请求方法
export const request = <T>(url: string, method: Method = 'GET', data?: object) => {
     return instance.request<any, Data<T>>({
       url,
       method,
       // 动态属性
       [method.toUpperCase() === 'GET'? 'params' : 'data'] : data
     }) 
}
```



### element

#### 插件导入中文包

- `main.js`中：

```js
import zhcn from 'element-plus/es/locale/lang/zh-cn'
```

- `index.js`中:

```js
app.use(main.ElementPlus, {
    locale: main.zhcn
})
```



#### 按需引入

1. 首先，安装 babel-plugin-component：

```bash
cnpm install babel-plugin-component -S
```

2. 在`babel-config.js`中替换：

```json
module.exports = {
  presets: [
    '@vue/cli-plugin-babel/preset',
    ["@babel/env", {"modules": false}]
  ],
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
}
```

3. 接下来，如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 element-ui.js 中写入以下内容：

```javascript
import {Button, Main} from 'element-ui'
import Vue from 'vue'


Vue.use(Button)
Vue.use(Main)
```





### element-plus

```
cnpm i element-plus --save
```



- `vite.config.ts`：

```js
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```



# 使用vite创建工程(Vue3)

## 配置开发环境和生产环境

![QQ截图20240522171242](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240522171242.png)

- 注意里面变量均要大写

![QQ截图20240522171351](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240522171351.png)





```
1. 创建工程
npm create vue@latest

2. 安装所需依赖
cnpm i


```



## 浏览器自动打开

- 在`package.json`中，修改dev命令：

```
"dev": "vite --open",
```





## 安装Vite-setup插件

```
cnpm i vite-plugin-vue-setup-extend -D
```



1. 在`vite.config.ts`中:

```js
import vueSetUp from 'vite-plugin-vue-setup-extend'

plugins: [
    vue(),
    vueSetUp()
  ],
```



## 安装TypeScript Vue Plugin

```js
cnpm install --save-dev typescript-vue-plugin


//tsconfig.json中配置
{
  "compilerOptions": {
    "plugins": [
      {
        "name": "typescript-vue-plugin"
      }
    ]
  }
}
```



## 自动本地持久化

1. 

```
cnpm i pinia-plugin-persistedstate
```

2. `main.ts`中：

```
import presist from 'pinia-plugin-persistedstate'

app.use(createPinia().use(presist))
```

3. 在仓库(store)中：

```typescript
export const useUserStore = defineStore("user", () => {
   
},{persist: true})   //配置该项
```



## 仓库的统一管理

1. 在`stores`文件夹中创建`modules`文件夹，存放所有仓库，并创建`index.ts`文件作为主要导出模块

<img src="https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240424164916.png" alt="QQ截图20240424164916" style="zoom:50%;" />

2. `index.ts`中统一管理`pinia`：（要在`main.ts`中引入该文件的pinia并`app.use(pinia)`）

```typescript
import { createPinia } from 'pinia'
import presist from 'pinia-plugin-persistedstate'

const pinia = createPinia()
pinia.use(presist)

export default pinia

export * from './modules/user'   //每有一个仓库，都从这里导入
```

3. 之后在组件中使用仓库时，直接：

```js
import { useUserStore } from './stores';
```



## 组件自动注册

```
cnpm i unplugin-vue-components -D
```

+ vite.config.ts中配置：

```typescript
// 二选一
import {ElementPlusResolver, VantResolver} from 'unplugin-vue-components/resolvers'

  plugins: [
    vue(),
    vueSetUp(),
    Components({
      // 不生成类型声明文件
      dts: false,
      resolvers: [
        // 二选一
        ElementPlusResolver(),  
        // importStyle: 不导入默认样式，只导入组件(可选)
        VantResolver({importStyle: false}) VantResolver()
      ],
    })
  ],
```



## 全局组件类型自动识别

- 在`types`下新建文件`components.d.ts`：

```typescript
import cpNavBar from "@/components/cpNavBar.vue";

declare module "vue" {
    interface GlobalComponents {
        //组件名 : typeof zu'jian
        CpNavBar: typeof cpNavBar;
    }
}
```



## 打包svg地图

```
cnpm i vite-plugin-svg-icons -D
```

![QQ截图20240429203102](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240429203102.png)



## svg组件封装

```vue
<template>
    <svg aria-hidden="true" class="cp-icon">
        <use :href="`#icon-${name}`"></use>
    </svg>
</template>

<script lang="ts" setup>

defineProps<{
    name: string
}>()

</script>
<style scoped lang="less">
.cp-icon {
    width: 1em;
    height: 1em;
    fill: currentColor;
    cursor: pointer;
}

</style>
```

+ **注：不要忘了注册全局组件！**

+ 使用：

```html
<cp-icon name="login-eye-off"/> 
```



## 修改加载进度条

```
cnpm i nprogress

cnpm i @type/nprogress -D   //vue3需装
```

+ 在`route.ts`中：

```typescript
import nProgress from 'nprogress'
import 'nprogress/nprogress.css'

nProgress.configure({ showSpinner: false })

// 路由前置守卫
router.beforeEach((to) => {
  nProgress.start()
  ......
})

// 路由后置守卫
router.afterEach((to) => {
  ......
  nProgress.done()
})
```

+ 注：可在全局样式文件`main.css`中修改进度条颜色

```css
#nprogress .bar {
  background-color: var(--cp-primary) !important;
}
```







## 移动端适配

```
cnpm i postcss-px-to-viewport -D
```

+ 新增配置文件`postcss.config.cjs`：

````js
module.exports = {
    plugins: {
        'postcss-px-to-viewport' : {
            viewportWidth: 375
        }
    }
}
````



### 获取设备宽度

```
cnpm i @vueuse/core
```



- 在需要使用设备宽度的地方导入即可

```js
import {useWindowSize} from "@vueuse/core";

const { width } = useWindowSize();
```





# Vue3语法

## Omit

```typescript
// Omit: 从User对象中排除token, avatar属性, 得到新类型
type OmitUser = Omit<User, 'token' | 'avatar'>;
```

+ 例如：现在要从`User`类型中排除`token`，并加上其他属性，得到新类型`UserInfo`，代码如下：

```typescript
type OmitUser = Omit<User, 'token'>;

export type UserInfo = OmitUser & {
    likeNumber: number; // 关注
    collectionNumber: number; // 收藏
    score: number; // 积分
    couponNumber: number; // 优惠券数量
    orderInfo:{
        paidNumber: number; // 待付款
        receivedNumber: number; // 待收货
        shippedNumber: number; // 待发货
        finishedNumber: number; // 已完成
    }
}
```





## 定义响应式数据

```js
<script lang="ts" setup name="person">
  import { ref } from "vue";
  import { reactive } from "vue";
  
  let name = ref('张三')                      //定义基本类型
  
  let obj = reactive({name:'李四', age: 13})  //定义对象类型
  let obj2 = reactive([
    {name:'李四', age: 13},
    {name:'李四', age: 13},
    {name:'李四', age: 13}
  ])

  function change_name() {
      name.value = '王五'
  }
</script>
```

- 区别：

![QQ截图20240113152803](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240113152803.png)

例：

![QQ截图20240113152850](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240113152850.png)



## toRefs

- 解构赋值的时候需要使用，将结构出来的值变为响应式数据

```vue
<template>
  <h1>{{ obj2.name + obj2.age }}</h1> 
  <button @click="change_name">修改姓名</button>
</template>

<script lang="ts" setup name="person">
  import { ref, toRefs } from "vue";
  import { reactive } from "vue";
  
  let obj2 = reactive(
    {name:'李四', age: 13}
  )

  let {name, age} = toRefs(obj2) //将解构出来的值变为响应式数据

  function change_name() {
      name.value = '王五',  //注意修改时用value
      age.value += 1        //修改结构数据时，原数据也会变
  }
</script>

```



## computed

```vue
<template>
  <h1>{{ obj2.name + obj2.age }}</h1> 
  <h1>{{ "计算属性:" + cpt}}</h1> 
  <br>
  <button @click="change_name">修改姓名</button>
</template>

<script lang="ts" setup name="person">
  import {toRefs, computed } from "vue";
  import { reactive } from "vue";
  
  let obj2 = reactive(
    {name:'李四', age: 13}
  )

  let {name, age} = toRefs(obj2) 
  
  let cpt = computed(() => {       //计算属性
      return name.value + age.value
  })

  function change_name() {
      name.value = '王五',  //注意修改时用value
      age.value += 1        //修改结构数据时，原数据也会变
  }
</script>

```



## watch

```vue
<template>
  <h1>{{ obj2.name + obj2.age }}</h1> 
  <h1>{{ "计算属性:" + cpt}}</h1> 
  <br>
  <button @click="change_name">修改姓名</button>
</template>

<script lang="ts" setup name="person">
  import {toRefs, computed, watch } from "vue";
  import { reactive } from "vue";
  
  let obj2 = reactive(
    {name:'李四', age: 13}
  )

  let {name, age} = toRefs(obj2) 
  
  let cpt = computed(() => {       //计算属性
      return name.value + age.value
  })

  watch(age, (newVal, oldVal) => {  //监视器
      console.log('监视器');
      
  })

  function change_name() {
      name.value = '王五',  //注意修改时用value
      age.value += 1        //修改结构数据时，原数据也会变
  }



</script>

```

### 解除监视

```js
  const stopWatch = watch(age, () => {  //监视器
      console.log('监视器');
      if(age.value > 20) stopWatch()  //解除监视
  })
```



### 监视ref定义的对象类型

![QQ截图20240114145559](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240114145559.png)

```js
  let obj2 = ref(
    {name:'李四', age: 13}
  )

  //开启深度监视
  watch(obj2, (newVal, oldVal)=>{
      obj2.value.name = '王五',
      obj2.value.age = 20
  }, {deep:true})

```

- **注意：若只修改对象类型中的属性，而不是修改整个对象，`oldVal 和 newVal`是一样的！**
- **本质：地址值没变，只有地址变了，两者才会不同！**



### 监视reactive定义的对象类型

- 默认开启深度监视，且无法关闭



### 监视对象的某个属性

```js
 let obj2 = reactive(
   {name:'李四', age: 13}
 )

watch(()=>obj2.name, (newVal, oldVal)=>{
    console.log('name变化了');
    
})
```

- **监视对象必须写成函数类型！**
- 若该属性是对象类型，即对象中的对象，则需要加上深度监视`deep`



### 监视多个数据

![QQ截图20240114152705](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240114152705.png)



## watchEffect

![QQ截图20240114154849](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240114154849.png)

- **注：页面打开时会自动调用一次函数**



## ref代替id打标识

![QQ截图20240114155646](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240114155646.png)

- **注：当对子组件使用`ref`时，若要拿到子组件的值，必须要在子组件中说明！如，父组件访问子组件中的`a, b, c`，最后要在子组件中写如下函数：**

![QQ截图20240114160307](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240114160307.png)



## 定义接口，自定义类型

- 在`src/`中创建一个`types`文件夹储存所有接口类型

```js
//定义接口，用于限制对象属性
export interface Person {
    id: string,
    name: string,
    age: number,
    x?: string    // ?表示可有可无
}

//定义自定义类型
export type Persons = Array<Person>  //Person数组
```

- `vue`中引入

```vue
<template>
    <h1>{{ person.id }}</h1>
    <h1>{{ person.name }}</h1>
    <h1>{{ person.age }}</h1>
</template>

<script lang="ts" setup>
import { type Person, type Persons } from "@/types"
import { ref, reactive } from "vue";

let person = ref<Person>({
    id: '1232187',
    name: '你好',
    age: 30
})

let personList = reactive<Persons>([
    {
        id: '1232187',
        name: '你好',
        age: 30
    },
    {
        id: '1232187',
        name: '你好',
        age: 30
    }
])



</script>

```



## hooks

- 在`src`下创建`hooks`目录
- 命名规范：`useXxx.ts`
- 内容:

```js
import { type Person, type Persons } from "@/types"
import { ref, reactive } from "vue";

export default function(){
    let person = ref<Person>({
        id: 'aaa',
        name: '你好',
        age: 30
    })
    
    let personList = reactive<Persons>([
        {
            id: '1232187',
            name: '你好',
            age: 30
        },
        {
            id: '1232187',
            name: '你好',
            age: 30
        }
    ])
    
    function personFunc(){
        person.value.age++
    }

    //向外部提供
    return {person, personList, personFunc}
}


```



- 使用：

```vue
<template>
    <h1>{{ person.id }}</h1>
    <h1>{{ person.name }}</h1>
    <h1>{{ person.age }}</h1>
</template>

<script lang="ts" setup>
import usePerson from "@/hooks/usePerson"
const {person, personFunc, personList} = usePerson()
</script>
```



## 路由

- `main.ts`中：

```js
import router from './router'

const app = createApp(App)

app.use(router)

app.mount('#app')
```

- 创建`router`目录，中创建`index.ts`
- `index.ts`：

```js
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',  //主页面
      name: 'home',
      component: HomeView
    },
    {
      path: '/about',
      name: 'about',
      component: () => import('../views/AboutView.vue')
    }
  ]
})

export default router

```

- `App.vue`中：

```vue
<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import {  } from "vue";
</script>

<template>
  <!-- 路由组件占位 -->
  <RouterView /> 
</template>
```



### meta.env.BASE_URL

![QQ截图20240408203149](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240408203149.png)



### 嵌套路由

```js
routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView,
      children:[
        {
          path:'child',
          component: () => import('../views/AboutView.vue')
        }
      ]
    },
```

- 注意子路由也要占位!



### 路由传参

- `query`传参：可在`url`中看到参数

	- 写法：

	```vue
	//routes中
	
	{
	      path: '/:key1/:key2?',    //加?表示可传可不传
	      name: 'home',
	      component: HomeView,
	      children:[
	        {
	          path:'child',
	          component: () => import('../views/AboutView.vue')
	        }
	      ]
	    },
	        
	
	//组件：
	<RouterLink to="/child/你好/我好">About</RouterLink
	```

	- 接收参数：

```js
import { useRoute } from "vue-router";
let route = useRoute()

//页面
<div>{{ route.query.key }}</div>

```

- `param`传参：无法在`url`中看到参数
	- 写法：

```html
<RouterLink :to="{
          name:'name',   //注意只能用name
          param:{
            key1: value1,
            key2: value2
          }
        }">Home</RouterLink>
```

![QQ截图20240118101404](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118101404.png)



### props

- param传参：

```js
//路由规则
{
      path: '/:key1/:key2',
      name: 'home',
      component: HomeView,
      children:[
        {
          path:'child',
          props: true,     //加上这一项
          component: () => import('../views/AboutView.vue')
        }
      ]
},
    
//组件中
defineProps(['key1', 'key2']) 

```



### 编程式导航

```js
import { useRouter } from "vue-router"
const router = useRouter()
onMounted(() => {
    router.push('/news')
    //或
    router.push({
      path:'url',
      name:'你好',
      params:{
        key1: '你好',
        key2: '我好'
      }
    })
})

//设置接口
interface newsInter{
    id: string,
    content: string
}

// 在函数中使用
function func(news:newsInter){
  router.push({
      path:'url',
      name:'你好',
      params:{
        key1: news.id,
        key2: news.content
      }
    })
}
```

- 注意是`useRouter`，不是`useRoute`



### 重定向

```js
{
  path:'/',
  redirect: '/home'
}
```



### 路由守卫

```typescript
// 路由前置守卫(设置访问权限)
router.beforeEach((to) => {
  // 获取token
  const store = useUserStore();
  // 白名单
  const whiteList = ['/login', '/home'];
  console.log(store.user);
  
  // 未登录且不在白名单，跳转登录页
  if(!store.user?.token && !whiteList.includes(to.path)) return '/login'

  // 放行
})

// 路由后置守卫(设置页面标题)
router.afterEach((to) => {
  // 设置页面标题(要先在路由中的meta属性中添加title属性)
  document.title = `${to.meta.title}` || 'Doctor Patients'
})

```



## slot插槽

### 默认插槽

- 父组件中（使用插槽）：

![QQ截图20240118155922](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118155922.png)



- 子组件中（定义插槽）：

![QQ截图20240118160054](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118160054.png)

- `<slot>`位置就会被替代。（可以增加默认标签）



### 具名插槽

- 父组件

![QQ截图20240118160919](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118160919.png)

- 子组件：

![QQ截图20240118160812](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118160812.png)



### 作用域插槽

- 子组件：

![QQ截图20240118161853](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118161853.png)

- 父组件：

![QQ截图20240118161913](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118161913.png)

- 注意：
	- params包含了子组件传递的所有参数
	- 若插槽带有名字，则作用域插槽也要指定名字

![QQ截图20240118162355](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118162355.png)



- 也可以解构值：

![QQ截图20240118162024](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118162024.png)



## toRaw

- 作用：将响应式数据变回原始的数据类型
- 用于axios中的参数传递

```js
import { toRaw } from "vue";

const {data:res} = await this.$axios({
    method: 'post',
    url: '/api/tickets/changedate',
    data: toRaw(car)
  })
```



## subspense

- 作用：当组件的数据需要发送异步请求，没有返回数据时，需要展示其他页面，可用该组件，例如实现显示加载中。。。的功能

![QQ截图20240118192621](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118192621.png)



## 组件通信

### props（父传子）

- 父组件中写法不变

```html
<child :car = "car"/>
```

- 子组件写法：

```js
//接受父组件传值list，并限制元素类型
defineProps<{list:Persons}>()

//接受父组件传值list，并限制元素类型和必要性（默认为必须要有, 有？为可有可无）
defineProps<{list?:Persons}>()

//接受父组件传值list，并限制元素类型，指定默认值
withDefaults(defineProps<{list:Persons}>(), {
    list:() => [{id:'1', name:'你好', age:13}]
})
```



### custon-event自定义事件（子传父）

- 父组件

```html
<child @haha="xxx"/>
```

- 子组件

```js
const emit = defineEmits(['haha'])
function func2(){
    emit('haha')
}
```



### mitt（任意组件传值）

- 安装：

```
cnpm i mitt
```



- 创建一个`utils/emitter.ts`文件

```js
import mitt from 'mitt'

const emitter = mitt()

//绑定事件
emitter.on('test', (val)=>{
    alert(val)
})

//触发事件
emitter.emit('test', 6)

//解绑事件
emitter.off('test')



export default emitter

```

- 在组件中：

```js
import emitter from './utils/emitter'
```



### $attrs（祖孙通信）

```vue
//父组件
<child :car="car"/>

//子组件
<child v-bind="$attrs"/>

//孙组件
使用defineProps接收数据
```



### $refs

- **注意：要用`defineExpose`将数据暴露**

```vue
  <child ref="c1"/>
  <child ref="c2"/>
  <button @click="func3($refs)"></button>


function func3(refs: any){
    for(let key in refs) 
      refs[key].value = 3
    
}
```



### $parent

- 用法与`$refs`相同，用于获取和修改父组件的数据



### provide

- 向所有后代提供数据

- 父组件中：

```js
import { provide } from 'vue';

provide('car', car) //注意不能.value，否则传入的数据不是响应式

```

- 后代组件中：

```js
import { inject } from 'vue';

let car2 = inject('car', {brand: '', price: 0}) //第二个参数为默认值
```







# pinia

- 安装

```
cnpm i pinia
```

- 导入

```js
//main.ts中

import { createPinia } from "pinia"
const pinia = createPinia()
app.use(pinia)
```

- 使用
	- 在`src`下创建文件夹`store`

![QQ截图20240118113839](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240118113839.png)

```js
import { defineStore } from 'pinia'
import {Ref, ref} from 'vue'
import {User} from "../types/user";

const useUserStore = defineStore('user', () => {
    const user:Ref<User | null> = ref(null)
    const saveUser = (newUser: User) => {
        user.value = newUser
    }
    return {user, saveUser}
})

export default useUserStore
```

## 读数据

```js
import { useCountStore } from "@/store/count"
import { storeToRefs } from 'pinia';

const countStore = useCountStore()
const {sum} = storeToRefs(countStore)

//标签
<div>{{ sum }}</div>
```

## 修改数据

- 方式一：

- ```
	直接改:
	countStore.sum += 1
	```

- 方式二：

- ```
	批量更改:
	function func(){
	  countStore.$patch({
	    sum: 999
	  })
	}
	```

- 方式三：

- ```js
	export const useCountStore = defineStore('count', {
	    state(){
	        return{
	            sum:6
	        }
	    },
	
	    actions:{
	        add(value: number){
	            if(this.sum < 10)
	                this.sum = value
	        }
	    }
	})
	
	//使用
	countStore.add(9)
	```



## 计算属性：getters

- ```
	    state(){
	        return{
	            sum:6
	        }
	    },
	
	    getters:{
	        sum2: state => state.sum + 6
	    }
	```

- 使用时和`state`一样



## 监视器：$subscribe

- 可用于存储用户信息。

```js
//组件中
countStore.$subscribe((mutate, state) => {
      sessionStorage.setItem('sum', JSON.stringify(state.sum))
})

//pinia中
import { type User } from "@/types"

	 state(){
        return{
            sum:6,
            user: JSON.parse(sessionStorage.getItem('user') as string) as User || {}
         	//前面只能写as string，后面as User是限定类型 
        }
    },
```















# less

- 安装：`cnpm i less -S`



## 运算

* 加、减、乘直接书写计算表达式
* 除法需要添加 小括号 或 .
* 表达式存在多个单位以第一个单位为准

![1681811616094](https://vip.123pan.cn/1828962653/md-images/vue.assets/1681811616094.png)

嵌套

作用：快速生成后代选择器

![1681811640347](https://vip.123pan.cn/1828962653/md-images/vue.assets/1681811640347.png)

提示：用 & 表示当前选择器，不会生成后代选择器，通常配合伪类或伪元素使用

![1681811659709](https://vip.123pan.cn/1828962653/md-images/vue.assets/1681811659709.png)

## 变量

概念：容器，存储数据

作用：存储数据，方便使用和修改

语法：

* 定义变量：@变量名: 数据; 
* 使用变量：CSS属性：@变量名;

```less
// 定义变量
@myColor: pink;
// 使用变量
.box {
  color: @myColor;
}
a {
  color: @myColor;
}
```

## 导入

作用：导入 less 公共样式文件

语法：导入: @import “文件路径”;

提示：如果是 less 文件可以省略后缀

```less
@import './base.less';
@import './common';
```

## 导出

写法：在 less 文件的第一行添加 // out: 存储URL

提示：文件夹名称后面添加 /

```less
// out: ./index.css
// out: ./css/
```

## 禁止导出

写法：在 less 文件第一行添加:  // out: false 

![1681811772496](https://vip.123pan.cn/1828962653/md-images/vue.assets/1681811772496.png)

# 技巧

## 全选和取消全选使用计算属性

![QQ截图20240330204513](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330204513.png)



![QQ截图20240330204628](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330204628.png)

![QQ截图20240330204648](https://vip.123pan.cn/1828962653/md-images/vue.assets/QQ截图20240330204648.png)



- 注：**`v-model`不能绑定`props`中的值**，因为`props`中的值只读，无法修改



## 实现上方导航条(移动端)

```VUE
<template>
    <VanNavBar id="topNavBar" 
    fixed 
    left-arrow 
    :title="title" 
    :right-text="rightText"
    @click-left="clickLeft"
    @click-right="clickRight"></VanNavBar>
    <div style="height: 60px;"></div>
</template>

<script lang="ts" setup>
import router from "@/router";
import { ref, reactive } from "vue"

const props = defineProps<{
    title?: string,
    rightText?: string
    back?: () => void
}>()

const emit = defineEmits<{
    (e : "click-right"): void
}>()

 const clickRight = () => {
    emit("click-right")
 }

 // 实现回退
const clickLeft = () => {

    if(props.back) return props.back()

    if(history.state?.back){    // 有历史记录
        router.back()
    }else{   // 无历史记录
        router.push('/')
    } 
}

</script>
<style lang="scss">

    #topNavBar {
        & .van-icon{
            color: var(--cp-text1);
            font-size: 18px;
        }

        & .van-nav-bar__title {
            font-size: 15px;
        }
    }
</style>

```



## 自定义单选按钮组件封装

```vue
<template>
    <van-row justify="space-around" id="radio-btn">
        <van-button 
        v-for="item in options" :key="item.value" 
        type="primary" 
        @click="$emit('update:modelValue', item.value)"
        :plain="item.value !== modelValue">
        {{ item.label }}
    </van-button>
    </van-row>
</template>

<script lang="ts" setup>
import { ref, reactive } from "vue"

defineProps<{
    options: { label: string, value: number }[],
    modelValue: number
}>()

defineEmits<{
    (e: 'update:modelValue', value: number) : void
}>()

</script>
<style lang="less">
#radio-btn {
    .van-button{
        width: 90px;
        height: 40px;
        font-size: 13px;
    }
}
</style>
```

+ 使用：

```html
<CpRadioBtn :options="radioOptions" v-model="gender"></CpRadioBtn>
```





```typescript
// 将一个对象的所有属性全部设为可选
type PartialConsult = Partial<Consult>
```





## showConfirmDialog

+ 若需要在页面回退时不自动关闭弹窗，需要修应一个属性

```typescript
showConfirmDialog({
            title: '温馨提示',
            message: '是否要恢复上一次填写的内容？',
            closeOnPopstate: false, // 是否在页面回退时自动关闭
        }).then(() => {
            const { illnessDesc, illnessTime, consultFlage, pictures } = store.consult;
            form.value = { illnessDesc, illnessTime, consultFlage, pictures }
            fileList.value = pictures || [];
        })
```



## 获取自定义类型中的所有类型

```typescript
type Key = keyof Partial<Consult>;

    const validKeys : Key[] = [
        'consultFlage',
        'couponId',
        'illnessTime',
        'illnessDesc',
        'depId',
        'patientid',
        'type'
    ] 
```

