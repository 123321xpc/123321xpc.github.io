---
title: margin的负值和塌陷问题
published: 2024-05-18
description: ''
image: ''
tags: [margin]
category: '各类问题'
draft: false 
---



# margin的纵向重叠

```html
	<style>
        p {
            font-size: 16px;
            line-height: 1;
            margin-top: 10px;
            margin-bottom: 15px;
        }
    </style>

    <p>AAA</p>
    <p></p>
    <p></p>
    <p></p>
    <p>BBB</p>
```

上述代码中，`AAA`和`BBB`的距离是多少？  `15px`



+ 相邻元素的`margin-top 和 margin-bottom`会重叠（取大）,**横向不会重叠！**
+ 而空白内容也会重叠
+ **故上述答案为15px**    



# margin负值问题

+ `margin-top `和`margin-left`为负值，元素自身会向上，左移动
+ `margin-bottom `和`margin-right`为负值，元素自身不受影响，下方元素会朝上移动，右侧元素朝左移动。（吸附）

