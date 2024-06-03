---
title: bfs的理解和应用
published: 2024-05-18
description: ''
image: ''
tags: [bfs]
category: '各类问题'
draft: false 
---





# BFS的理解和引用

+ 内部元素的渲染不会影响外部元素
+ 形成BFC的常见条件：
	+ **float 不是 none**
	+ **position是 absolute 或fixed**
	+ **overflow 不是visible**
	+ **display 是 flex或inline-block**
+ 常见应用
	+ 清除浮动：有时候，给图片设置浮动，会导致图片不会撑大容器，而是跑到容器外部，也叫脱离文档流。如图：

![QQ截图20240518230831](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/bfs.assets/QQ%E6%88%AA%E5%9B%BE20240518230831.png)

+ 解决：使之形成BFC，给图片添加属性`overflow: hidden`即可，如下图：

![QQ截图20240518230916](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/bfs.assets/QQ%E6%88%AA%E5%9B%BE20240518230916.png)
