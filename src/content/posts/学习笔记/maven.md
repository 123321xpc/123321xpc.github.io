---
title: maven 学习笔记
published: 2024-05-17
description: ''
image: ''
tags: [学习笔记, maven]
category: '学习笔记'
draft: false
---

- [基础配置](#基础配置)
  - [配置本地仓库](#配置本地仓库)
  - [配置阿里云提供的镜像仓库](#配置阿里云提供的镜像仓库)
    - [①将原有的例子配置注释掉](#将原有的例子配置注释掉)
    - [②加入我们的配置](#加入我们的配置)
  - [配置 Maven 工程的基础 JDK 版本](#配置-maven-工程的基础-jdk-版本)
  - [配置 MAVEN\_HOME](#配置-maven_home)
  - [配置PATH](#配置path)
  - [验证](#验证)
- [依赖范围](#依赖范围)
  - [①compile 和 test 对比](#compile-和-test-对比)
  - [②compile 和 provided 对比](#compile-和-provided-对比)
  - [③结论](#结论)
- [依赖传递](#依赖传递)
- [依赖排除](#依赖排除)
- [继承](#继承)
  - [①创建父工程](#创建父工程)
  - [④子工程的pom.xml](#子工程的pomxml)
  - [⑤在父工程中配置依赖的统一管理](#在父工程中配置依赖的统一管理)
  - [⑥子工程中引用那些被父工程管理的依赖](#子工程中引用那些被父工程管理的依赖)
  - [⑦在父工程中升级依赖信息的版本](#在父工程中升级依赖信息的版本)
- [自定义属性](#自定义属性)
- [聚合](#聚合)
  - [聚合的配置](#聚合的配置)


## 基础配置

### 配置本地仓库

本地仓库默认值：用户家目录/.m2/repository。由于本地仓库的默认位置是在用户的家目录下，而家目录往往是在 C 盘，也就是系统盘。将来 Maven 仓库中 jar 包越来越多，仓库体积越来越大，可能会拖慢 C 盘运行速度，影响系统性能。所以建议将 Maven 的本地仓库放在其他盘符下。配置方式如下：

```XML
<!-- localRepository
| The path to the local repository maven will use to store artifacts.
|
| Default: ${user.home}/.m2/repository
<localRepository>/path/to/local/repo</localRepository>
-->
<localRepository>D:\maven-repository</localRepository>
```

本地仓库这个目录，我们手动创建一个空的目录即可。

记住：一定要把 localRepository 标签从注释中拿出来。

注意：本地仓库本身也需要使用一个非中文、没有空格的目录。



### 配置阿里云提供的镜像仓库

Maven 下载 jar 包默认访问境外的中央仓库，而国外网站速度很慢。改成阿里云提供的镜像仓库，访问国内网站，可以让 Maven 下载 jar 包的时候速度更快。配置的方式是：

#### ①将原有的例子配置注释掉

```XML
<!-- <mirror>
  <id>maven-default-http-blocker</id>
  <mirrorOf>external:http:*</mirrorOf>
  <name>Pseudo repository to mirror external repositories initially using HTTP.</name>
  <url>http://0.0.0.0/</url>
  <blocked>true</blocked>
</mirror> -->
```



#### ②加入我们的配置

将下面 mirror 标签整体复制到 settings.xml 文件的 mirrors 标签的内部。

```XML
  <mirror>
    <id>nexus-aliyun</id>
    <mirrorOf>central</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
  </mirror>
```

### 配置 Maven 工程的基础 JDK 版本

如果按照默认配置运行，Java 工程使用的默认 JDK 版本是 1.5，而我们熟悉和常用的是 JDK 1.8 版本。修改配置的方式是：将 profile 标签整个复制到 settings.xml 文件的 profiles 标签内。

```XML
  <profile>
    <id>jdk-1.8</id>
    <activation>
    <activeByDefault>true</activeByDefault>
    <jdk>1.8</jdk>
    </activation>
    <properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
    </properties>
  </profile>
```

### 配置 MAVEN_HOME

![image](https://vip.123pan.cn/1828962653/md-images/学习笔记/maven.assets/image.png)



### 配置PATH

![image-17067840043351](https://vip.123pan.cn/1828962653/md-images/学习笔记/image-17067840043351.png)



### 验证

```Bash
mvn -v
```



## 依赖范围

- 标签：`<scope>`
- 标签的可选值：
  - compile
  - test
  - provided

### ①compile 和 test 对比

|         | main目录（空间） | test目录（空间） | 开发过程（时间） | 部署到服务器（时间） |
| ------- | ---------------- | ---------------- | ---------------- | -------------------- |
| compile | 有效             | 有效             | 有效             | 有效                 |
| test    | 无效             | 有效             | 有效             | 无效                 |




### ②compile 和 provided 对比

|          | main目录（空间） | test目录（空间） | 开发过程（时间） | 部署到服务器（时间） |
| -------- | ---------------- | ---------------- | ---------------- | -------------------- |
| compile  | 有效             | 有效             | 有效             | 有效                 |
| provided | 有效             | 有效             | 有效             | 无效                 |




### ③结论

**compile**：通常使用的第三方框架的 jar 包这样在项目实际运行时真正要用到的 jar 包都是以 compile 范围进行依赖的。比如 **SSM 框架所需jar包**。  

**test**：测试过程中使用的 jar 包，以 test 范围依赖进来。比如 **junit, spring-test**。  

**provided**：在开发过程中需要用到的“服务器上的 jar 包”通常以 provided 范围依赖进来。比如 **servlet-api、jsp-api**。而这个范围的 jar 包之所以不参与部署、不放进 war 包，就是避免和服务器上已有的同类 jar 包产生冲突，同时减轻服务器的负担。说白了就是：“服务器上已经有了，你就别带啦！”  



## 依赖传递

​		在 A 依赖 B，B 依赖 C 的前提下，C 是否能够传递到 A，取决于 B 依赖 C 时使用的依赖范围。

- B 依赖 C 时使用 compile 范围：可以传递
- B 依赖 C 时使用 test 或 provided 范围：不能传递。



## 依赖排除

```xml
<dependency>
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro01-maven-java</artifactId>
  <version>1.0-SNAPSHOT</version>
  <scope>compile</scope>
  <!-- 使用excludes标签配置依赖的排除  -->
  <exclusions>
    <!-- 在exclude标签中配置一个具体的排除 -->
    <exclusion>
      <!-- 指定要排除的依赖的坐标（不需要写version） -->
      <groupId>commons-logging</groupId>
      <artifactId>commons-logging</artifactId>
    </exclusion>
  </exclusions>
</dependency>

```



## 继承

### ①创建父工程

```XML
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro03-maven-parent</artifactId>
  <version>1.0-SNAPSHOT</version>

  <!-- 当前工程作为父工程，它要去管理子工程，所以打包方式必须是 pom -->
  <packaging>pom</packaging>
```

​		只有打包方式为 pom 的 Maven 工程能够管理其他 Maven 工程。打包方式为 pom 的 Maven 工程中不写业务代码，它是专门管理其他 Maven 工程的工程。



```XML
<modules>  
  <module>pro04-maven-module</module>
  <module>pro05-maven-module</module>
  <module>pro06-maven-module</module>
</modules>

```



### ④子工程的pom.xml

```XML
<!-- 使用parent标签指定当前工程的父工程 -->
<parent>
  <!-- 父工程的坐标 -->
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro03-maven-parent</artifactId>
  <version>1.0-SNAPSHOT</version>
</parent>

<!-- 子工程的坐标 -->
<!-- 如果子工程坐标中的groupId和version与父工程一致，那么可以省略 -->
<!-- <groupId>com.atguigu.maven</groupId> -->
<artifactId>pro04-maven-module</artifactId>
<!-- <version>1.0-SNAPSHOT</version> -->
```



### ⑤在父工程中配置依赖的统一管理

```XML
<!-- 使用dependencyManagement标签配置对依赖的管理 -->
<!-- 被管理的依赖并没有真正被引入到工程 -->
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```

### ⑥子工程中引用那些被父工程管理的依赖

关键点：省略版本号

```XML
<!-- 子工程引用父工程中的依赖信息时，可以把版本号去掉。  -->
<!-- 把版本号去掉就表示子工程中这个依赖的版本由父工程决定。 -->
<!-- 具体来说是由父工程的dependencyManagement来决定。 -->
<dependencies>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-expression</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
  </dependency>
</dependencies>
```



### ⑦在父工程中升级依赖信息的版本

```XML
……
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>4.1.4.RELEASE</version>
      </dependency>
……
```



## 自定义属性

```XML
<!-- 通过自定义属性，统一指定Spring的版本 -->
<properties>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  
  <!-- 自定义标签，维护Spring版本数据 -->
  <atguigu.spring.version>4.3.6.RELEASE</atguigu.spring.version>
</properties>
```

- 在需要的地方使用${}的形式来引用自定义的属性名：

```XML
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>${atguigu.spring.version}</version>
      </dependency>
```



## 聚合

### 聚合的配置

在**父工程**中配置 modules 即可：

```XML
  <modules>  
    <module>pro04-maven-module</module>
    <module>pro05-maven-module</module>
    <module>pro06-maven-module</module>
  </modules>
```
