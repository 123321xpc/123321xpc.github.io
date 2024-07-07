---
title: springboot项目指定全局接口添加前缀
published: 2024-07-07
description: ''
image: ''
tags: [各类问题, springboot]
category: '各类问题'
draft: false 
---





在配置文件中加入如下配置：

```yaml
server:
  servlet:
    context-path: /api
```

可以使该项目所有的接口加上`/api`前缀
