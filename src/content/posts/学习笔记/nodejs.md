---
title: nodejs 学习笔记
published: 2024-05-16
description: ''
image: ''
tags: [学习笔记, nodejs]
category: '学习笔记'
draft: false
---


- [为什么Javascript能在浏览器中执行？](#为什么javascript能在浏览器中执行)
- [浏览器中Javascript的运行环境](#浏览器中javascript的运行环境)
- [Nodejs中的Javascript的运行环境](#nodejs中的javascript的运行环境)
- [fs文件系统模块](#fs文件系统模块)
  - [fs.readFile(url, \[codetype\], callback)](#fsreadfileurl-codetype-callback)
  - [fs.writeFile(url, data, \[codetype\], callback)](#fswritefileurl-data-codetype-callback)
  - [fs.existsSync(url)](#fsexistssyncurl)
  - [练习](#练习)
- [path路径模块](#path路径模块)
  - [路径动态拼接问题](#路径动态拼接问题)
    - [解决办法：path.join(...\[string\])](#解决办法pathjoinstring)
  - [path.basename(url, \[后缀名\])](#pathbasenameurl-后缀名)
  - [path.extname(url)](#pathextnameurl)
  - [path.parse(url)](#pathparseurl)
- [http模块](#http模块)
  - [创建基本的web服务器](#创建基本的web服务器)
  - [根据不同url返回不同内容](#根据不同url返回不同内容)
- [模块化](#模块化)
  - [分类](#分类)
  - [加载](#加载)
  - [模块作用域](#模块作用域)
  - [module对象](#module对象)
  - [module.exports 和exports](#moduleexports-和exports)
  - [CommonJS规范](#commonjs规范)
- [express](#express)
  - [安装及基本使用](#安装及基本使用)
  - [获取url中的query参数](#获取url中的query参数)
  - [获取动态参数](#获取动态参数)
  - [托管静态资源目录](#托管静态资源目录)
  - [托管多个静态资源目录](#托管多个静态资源目录)
  - [添加路径前缀](#添加路径前缀)
  - [路由](#路由)
    - [创建路由](#创建路由)
    - [路由模块化](#路由模块化)
  - [中间件](#中间件)
    - [格式](#格式)
    - [注意：普通中间件一定要在路由定义之前注册！！！](#注意普通中间件一定要在路由定义之前注册)
    - [定义中间件函数](#定义中间件函数)
    - [注册全局中间件函数](#注册全局中间件函数)
    - [定义多个全局中间件](#定义多个全局中间件)
    - [定义局部中间件](#定义局部中间件)
    - [使用多个局部中间件](#使用多个局部中间件)
    - [中间件分类](#中间件分类)
      - [应用级别的中间件](#应用级别的中间件)
      - [路由级别的中间件](#路由级别的中间件)
      - [错误级别的中间件](#错误级别的中间件)
      - [内置中间件](#内置中间件)
      - [第三方中间件](#第三方中间件)
  - [nodemon](#nodemon)
- [跨域](#跨域)
  - [Access-Control-Allow-Origin：解决跨域](#access-control-allow-origin解决跨域)
  - [Access-Control-Allow-Headers：发送额外请求头信息](#access-control-allow-headers发送额外请求头信息)
  - [Access-Control-Allow-Methods：使用其他方式发送请求](#access-control-allow-methods使用其他方式发送请求)
  - [请求分类](#请求分类)
    - [简单请求](#简单请求)
    - [预检请求](#预检请求)
    - [区别](#区别)
    - [JSONP请求](#jsonp请求)
- [JWT认证](#jwt认证)
  - [原理](#原理)
  - [使用方式](#使用方式)
  - [在express中使用JWT](#在express中使用jwt)
  - [获取用户信息](#获取用户信息)
  - [捕获解析JWT失败的错误](#捕获解析jwt失败的错误)





# 为什么Javascript能在浏览器中执行？

因为所有浏览器中都有一个专门解析`js`的解析引擎。

![QQ截图20240516134949](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516134949.png)



# 浏览器中Javascript的运行环境

![QQ截图20240516135403](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516135403.png)



`JS`可以调用浏览器提供的内置`DOM`和`BOM`的`API`来操作`BOM，DOM`，之后将代码交给解析引擎去执行。



# Nodejs中的Javascript的运行环境

![QQ截图20240516135832](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516135832.png)



> 注：`node.js`中无法调用`BOM`和`DOM`的内置`API`，因为没提供。



# fs文件系统模块

## fs.readFile(url, [codetype], callback)

- 功能：读取指定文件内容
- 参数：
	- `url`：文件路径
	- `codetype`：读取的编码格式，可选，默认为`utf-8`
	- `callback`：指定回调函数，用来获得读取结果

例：

```js
const { warn } = require('console');
const fs = require('fs')

fs.readFile('text.txt', 'utf8', (err, data) => {
    if (err) throw err;

    console.log(data);
})
```

若文件不存在，输出如下下：

![QQ截图20240516141302](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516141302.png)



若正常，输出文件内容：

![QQ截图20240516141340](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516141340.png)



> 如何判断文件是否读取成功？ 
>
>  若`err`的值不为null，则读取成功，为`null`，则读取失败。



## fs.writeFile(url, data, [codetype], callback)

- 功能：向指定文件写入内容
- 参数：
	- `utl`：要写入文件的路径（要加上后缀名），若文件不存在，则新建文件写入。
	- `data`：一般是`string`类型和`Buffer`类型
	- `callback`：回调函数，处理函数执行结果

例：

```js
const { warn } = require('console');
const fs = require('fs')

fs.writeFile('test1.txt', 'Hello, world!', (err) => {
  if (err) throw err;
  console.log('It\'s saved!');
});
```

输出如下：

![QQ截图20240516142016](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516142016.png)



## fs.existsSync(url)

- 作用：判断文件是否存在，返回结果为`true / false`

例：

```js
const exists = fs.existsSync('file.txt');
console.log(exists); // 输出 true 或 false
```



## 练习

![QQ截图20240516142146](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516142146.png)



代码如下：

```js
const { warn } = require('console');
const fs = require('fs')


fs.readFile('text.txt', (err, data) => {
    if(err) console.log('读取文件失败！');
    else{
        const arr = []

        // 处理字符串
        data.toString().split(" ").forEach(word => 
            arr.push(word.replace('=', ': '))
        )

        // 处理数组
        const res = arr.join('\n')

        fs.writeFile('./text1.txt', res, (err) => {
            if(err) console.log('写入文件失败！');
            else console.log('写入文件成功！');
        })
        
    }
})
```



> 注意：**写文件只能放在读文件的回调里面**，因为**读写文件是异步操作**，若要放外面，只能用`Promise`



# path路径模块

## 路径动态拼接问题

当路径是以`./`或`../`开头的相对路径时，会用执行`node`命令的路径拼接完整路径，从而导致错误。具体如下：

- 假设现在`text.txt`的绝对路径为：

```
C:\Users\ZhuanZ\Desktop\exerc\text.txt
```

- 在同目录下的`a.js`中，读取文件代码如下：

```js
fs.readFile('./text.txt', (err, data) => {
    if(err) console.log(err);
    else console.log('读取文件成功！');
})
```

- 当我在`exerc`，目录下运行命令`node .\a.js`，能成功读取文件，但当我到`Desktop`目录运行命令`node .\exerc\a.js`时，却读取不到文件，且错误信息如下：

![QQ截图20240516145437](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516145437.png)

- 可以看出：`nodejs`将运行命令时的绝对路径凭借到了相对路径上，所以没有拼接`exerc`目录。



### 解决办法：path.join(...[string])

- 作用：将传入的多个路径片段拼接。

![QQ截图20240516150020](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516150020.png)



- 上述问题代码可以改为如下：

```js
const { warn } = require('console');
const fs = require('fs')
const path = require('path')

const filePath = path.join(__dirname, 'text.txt')
fs.readFile(filePath, (err, data) => {
    if(err) console.log(err);
    else console.log('读取文件成功！');
})
```

这样就能读取到文件了。



## path.basename(url, [后缀名])

- 作用：获取`url`的文件名（若传入后缀名，则不获取，否则连后缀名一起获取）

例如：

```js
const path = require('path')

const url1 = './a/b/c/d.app'
console.log(path.basename(url1)) //输出d.app

const url2 = 'a/b/c/d.html/'
console.log(path.basename(url2)) //输出d.html
console.log(path.basename(url2, '.html')) //输出d
```



## path.extname(url)

- 作用：获取路径中的文件后缀名

例：

```js
const url2 = 'a/b/c/d.html/'
console.log(path.extname(url2)) //输出.html
```



## path.parse(url)

- 作用：将`url`中所有路径对象解析出来

例：

```js
const url1 = './a/b/c/d.app'
console.log(path.parse(url1)) 

const url3 = 'a:/b/c/d.app'
console.log(path.parse(url3)) 
```

结果如下：

![QQ截图20240516151351](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516151351.png)



> 注：相对路径没有根目录，所有目录都放在`dir`中



# http模块

## 创建基本的web服务器

```js
const http = require('http')
const server = http.createServer()

// 绑定监听请求，当有人访问服务器时，执行回调
server.on('request', (req, res) => {
    console.log('有人访问');

    // request对象包含了请求信息
    const url = req.url; // 获取请求的url(注意是端口号之后的地址)
    const method = req.method; // 获取请求的方法

    // response对象用于发送响应数据
    res.end('Hello World'); // 向客户端响应内容
    res.setHeader('Content-Type', 'text/html; charset=utf-8'); // 设置响应头信息(防止中文乱码)

})

// 启动服务器，监听80端口
server.listen(80, () => {
    console.log('服务器启动成功，监听80端口');
})
```



## 根据不同url返回不同内容

![QQ截图20240516155749](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240516155749.png)



# 模块化

## 分类

![QQ截图20240517133201](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517133201.png)



## 加载

```js
// 加载官方模块
const http = require('http');

// 加载自定义模块
const c = require('./c');

// 加载第三方模块
const axios = require('axios');
```



> 注意：1. 使用require加载模块，**会立刻执行模块中的代码**！
>
> ​			2. .js后缀名可以省略



## 模块作用域

在不暴露模块的前提下，模块内定义的成员无法被模块外的成员访问。



## module对象

每个模块都有一个自带的对象叫`module`，储存当前模块的信息，打印如下：

```json
{
  id: '.',
  path: 'C:\\Users\\ZhuanZ\\Desktop\\exerc',
  exports: {},
  filename: 'C:\\Users\\ZhuanZ\\Desktop\\exerc\\a.js',
  loaded: false,
  children: [],
  paths: [
    'C:\\Users\\ZhuanZ\\Desktop\\exerc\\node_modules',
    'C:\\Users\\ZhuanZ\\Desktop\\node_modules',
    'C:\\Users\\ZhuanZ\\node_modules',
    'C:\\Users\\node_modules',
    'C:\\node_modules'
  ]
}
```



## module.exports 和exports

![QQ截图20240517134509](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517134509.png)

![QQ截图20240517135708](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517135708.png)



## CommonJS规范

![QQ截图20240517135947](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517135947.png)



# express

## 安装及基本使用

- 安装包：

```
cnpm i express
```



- 使用：

```js
const express = require('express');
const app = express();

// 监听80端口
app.listen(80, () => {
    console.log('80端口被访问');
})

// 路由
app.get('/', (req, res) => {

    // 发送响应
    res.send('Hello World!');
})
```



## 获取url中的query参数

![QQ截图20240517141955](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517141955.png)



## 获取动态参数

![QQ截图20240517142158](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517142158.png)



## 托管静态资源目录

![QQ截图20240517142634](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517142634.png)



## 托管多个静态资源目录

![QQ截图20240517143014](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517143014.png)



## 添加路径前缀

![QQ截图20240517143310](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517143310.png)



## 路由

### 创建路由

![QQ截图20240517145508](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517145508.png)



### 路由模块化

![QQ截图20240517150408](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517150408.png)

路由添加前缀

![QQ截图20240517150704](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517150704.png)



## 中间件

### 格式

![QQ截图20240517151050](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517151050.png)



### 注意：普通中间件一定要在路由定义之前注册！！！



### 定义中间件函数

![QQ截图20240517151235](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517151235.png)



### 注册全局中间件函数

![QQ截图20240517151456](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517151456.png)



### 定义多个全局中间件

> 当有多个全局中间件时，会按照注册顺序依次调用。



![QQ截图20240517152213](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517152213.png)



### 定义局部中间件

![QQ截图20240517152439](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517152439.png)



### 使用多个局部中间件

![QQ截图20240517152720](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517152720.png)

> 注：中间件依次执行。



### 中间件分类

![QQ截图20240517153035](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517153035.png)



#### 应用级别的中间件

![QQ截图20240517153200](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517153200.png)



#### 路由级别的中间件

![QQ截图20240517153235](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517153235.png)



#### 错误级别的中间件

![QQ截图20240517153408](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517153408.png)



> 注意：错误级别的中间件必须定义在所有路由之后！！！



#### 内置中间件

![QQ截图20240517154008](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517154008.png)



#### 第三方中间件

![QQ截图20240517154500](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517154500.png)



## nodemon

- 作用：当使用nodejs编写web程序时，代码修改后，可自动重启项目。
- 安装：

```
cnpm i nodemon -g
```

- 使用：

```
nodemon app.js
```



# 跨域

## Access-Control-Allow-Origin：解决跨域

![QQ截图20240517154859](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517154859.png)

![QQ截图20240517154752](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517154752.png)



## Access-Control-Allow-Headers：发送额外请求头信息

![QQ截图20240517154823](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517154823.png)



## Access-Control-Allow-Methods：使用其他方式发送请求

![QQ截图20240517155024](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517155024.png)



## 请求分类

### 简单请求

![QQ截图20240517155236](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517155236.png)



### 预检请求

![QQ截图20240517155341](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517155341.png)



### 区别

![QQ截图20240517155428](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517155428.png)



### JSONP请求

![QQ截图20240517160238](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517160238.png)



![QQ截图20240517160318](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517160318.png)



# JWT认证

## 原理

![QQ截图20240517160655](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517160655.png)



## 使用方式

![QQ截图20240517160954](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517160954.png)



## 在express中使用JWT

- 安装

```
cnpm i jsonwebtoken express-jwt
```

- 导入

![QQ截图20240517161150](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517161150.png)

- 定义`secret`密钥

![QQ截图20240517161512](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517161512.png)

- 生成`JWT`字符串

![QQ截图20240517161612](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517161612.png)

- 解析`JWT`令牌

![QQ截图20240517161906](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517161906.png)



> 注：path数组中的字符串为正则表达式。



## 获取用户信息

![QQ截图20240517162416](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517162416.png)



> 注意：必须要使用`express-jwt`配置后才会有`req.user`对象！



## 捕获解析JWT失败的错误

![QQ截图20240517162511](https://vip.123pan.cn/1828962653/md-images/学习笔记/nodejs.assets/QQ%E6%88%AA%E5%9B%BE20240517162511.png)
