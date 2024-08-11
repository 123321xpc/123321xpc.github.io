---
title: idea卡在加载依赖
published: 2024-07-20
description: ''
image: ''
tags: [各类问题, maven]
category: '各类问题'
draft: false 
---



+ `idea`创建新项目时卡在`Resolving Maven dependencies`处很久



+ 解决方案：

	1. 修改镜像源

	```xml
	 <mirror>
	
	             <id>alimaven</id>
	              <name>aliyun maven</name>
	              <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
	              <mirrorOf>central</mirrorOf>        
	 </mirror>
	```

	2. 设置`idea`中`maven`配置`jvm`参数：`-Xms1024m -Xmx2048m`

	![image-20240720162234817](https://vip.123pan.cn/1828962653/md-images/idea卡在加载依赖.assets/image-20240720162234817.png)

	
