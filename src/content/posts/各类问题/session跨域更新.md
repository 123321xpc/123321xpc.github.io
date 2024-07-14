---
title: session跨域更新
published: 2024-07-14
description: ''
image: ''
tags: [session, java]
category: '各类问题'
draft: false 
---





# session, cookie跨域更新问题

+ 当项目跨域时，默认不允许请求访问。在后端配置`@CrossOrigin`注解后，前端可以访问，但不能携带`Cookie`，导致后端接收不到`Cookie`，就会为每个请求都生成新的`session`，导致`session`里的数据无法获取。
+ 若要访问带上`Cookie`，需要将`Access-Control-Allow-Credentials`设置为`true`。这样才能允许`CROS`从不同的域中接收`Cookie`



简单的解决办法是在每个`Controller`类上加注解

```
@CrossOrigin(originPatterns = "*", allowCredentials = "true")
```

并在前端`axios`上添加属性：允许携带`Cookie`

```
withCredentials: true
```

