---
title: 部分CSS题目
published: 2024-05-18
description: ''
image: ''
tags: [css, line-height, rem]
category: '各类问题'
draft: false 
---


- [line-height 如何继承？](#line-height-如何继承)
- [响应式](#响应式)
  - [rem是什么？](#rem是什么)
  - [vw / vh](#vw--vh)
  - [响应式布局常用方案](#响应式布局常用方案)



# line-height 如何继承？

- 若为普通px值，则直接继承，如`line-height: 20px`
- 若为倍数，则直接继承，如`line-height: 2`，如下：

```html
<style>

        body {
            font-size: 20px;
            line-height: 2;
        }

        p{
            font-size: 15px;
        }
</style>

<p>AAA</p>
```

上述代码中，行高为`30px`。



- 若为百分比，则先计算然后继承，具体如下：

```html
<style>
        body {
            font-size: 20px;
            line-height: 200%;
        }

        p{
            font-size: 15px;
        }
</style>

<p>AAA</p>
```

上述代码中，`<p>`的行高为`40px`

> 若将`body`中的字体大小删去，则行高变为`30px`



# 响应式

## rem是什么？

+ `rem`是一种相对长度单位，相对于根元素（`html`）。

如下所示：

```html
<style>
        html {
            font-size: 100px;
        }

        div{
            font-size: 0.5rem;
        }

        p {

            font-size: 0.7rem;
        }
</style>
```

+ 上述代码中，`div`标签的字体大小为`50px`，`p`标签为`70px`



## vw / vh

+ `1 vw / vh`：视口宽度 / 高度的百分之一

+ `window.screen.height`：屏幕高度
+ `window.innerHeight`：页面内容的高度

二者关系如下：

<img src="https://123321xpc-pictures.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/部分CSS题目.assets/QQ%E6%88%AA%E5%9B%BE20240518225314.png" alt="QQ截图20240518225314" style="zoom:67%;" />



## 响应式布局常用方案

1. 使用`media-query`，根据不同屏幕宽度设置`html`的`font-size`
2. 再使用`rem`做长度计算。



