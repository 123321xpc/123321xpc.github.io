---
title: http请求timeout设置问题
published: 2024-07-07
description: ''
image: ''
tags: [各类问题, 前端]
category: '各类问题'
draft: false 
---





**前端发送`http`请求时，若要设置`timeout`属性，不要设置得太短，至少为`5-10s`，否则会因为时间太短后端无法及时处理。前端接收不到响应数据而报错！！！**
