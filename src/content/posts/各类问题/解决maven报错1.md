---
title: 解决maven报错
published: 2024-05-17
description: '解决maven报错: java: 不再支持源选项 5。请使用 7 或更高版本。'
image: ''
tags: [maven, 解决报错]
category: '各类问题'
draft: false 
---


- [问题描述](#问题描述)
- [原因](#原因)
- [解决](#解决)





# 问题描述

使用`idea 2024`运行`springboot`工程时，控制台报如下错误：

```
java: 不再支持源选项 5。请使用 7 或更高版本
```



# 原因

在编译时，没有说明指定``JDK`版本号，`maven`默认指定了较低的5版本。



# 解决

在`maven`文件夹的`conf/setting.xml`文件中，添加如下配置，指定`JDK`版本即可。

```xml
<profiles>
    <profile>  
        <id>jdk-17</id>  
        <activation>  
           <activeByDefault>true</activeByDefault>  
           <jdk>17</jdk>  
        </activation>
        <properties>
           <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
           <maven.compiler.source>17</maven.compiler.source>  
           <maven.compiler.target>17</maven.compiler.target>   
        </properties>   
    </profile>
</profiles>
```

