---
title: git 学习笔记
published: 2024-05-12
tags: [git, 学习笔记]
category: 学习笔记
draft: false
---




## [常用命令](#常用命令)
- [常用命令](#常用命令-1)
  - [初始化本地仓库](#初始化本地仓库)
    - [方式一：克隆其他仓库（常用）](#方式一克隆其他仓库常用)
    - [方式二：在本地初始化新仓库](#方式二在本地初始化新仓库)
    - [文档更新记录](#文档更新记录)
  - [查看历史记录](#查看历史记录)
    - [只显示版本号和版本信息](#只显示版本号和版本信息)
    - [显示所有信息](#显示所有信息)
    - [显示所有版本（防止回退版本后再回到后面版本）](#显示所有版本防止回退版本后再回到后面版本)
  - [回退历史版本](#回退历史版本)
  - [状态查询](#状态查询)
- [分支操作](#分支操作)
  - [查看所有分支](#查看所有分支)
  - [创建新分支](#创建新分支)
  - [切换分支](#切换分支)
  - [修改分支名](#修改分支名)
  - [删除分支](#删除分支)
  - [合并分支](#合并分支)
- [推送到远程仓库（gitee为例）](#推送到远程仓库gitee为例)
  - [1. 先在gitee上创建新仓库](#1-先在gitee上创建新仓库)
  - [2. 在本地项目文件夹中关联远程仓库](#2-在本地项目文件夹中关联远程仓库)
  - [3. 将本地文件推送到远程仓库](#3-将本地文件推送到远程仓库)
    - [第一次提交](#第一次提交)
    - [之后提交](#之后提交)
  - [修改关联的远程仓库](#修改关联的远程仓库)
  - [仓库克隆](#仓库克隆)
  - [仓库拉取](#仓库拉取)
- [SSH免密登录](#ssh免密登录)
  - [1. 生成ssh公钥](#1-生成ssh公钥)
  - [2. 查看及拷贝公钥](#2-查看及拷贝公钥)
  - [测试激活公钥](#测试激活公钥)
- [.gitignore 忽略文件](#gitignore-忽略文件)
  - [语法](#语法)
- [VSCode中的git](#vscode中的git)
- [显示隐藏文件夹](#显示隐藏文件夹)



# 常用命令

``` 
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

- **查看配置：**（按q退出）

```
git config --list
```



## 初始化本地仓库

### 方式一：克隆其他仓库（常用）

```
git clone 仓库地址
```

### 方式二：在本地初始化新仓库

在你要提交的文件夹中打开终端，输入命令：

```
git init
```

- 成功标志：文件夹中出现`.git`文件夹（需要[显示隐藏文件夹](#显示隐藏文件夹)）



### 文档更新记录

当你完成一个阶段的任务后，想要保存，就可以提交到仓库。

git的区域主要分为以下三块：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512113449.png" alt="QQ截图20240512113449" style="zoom:50%;" />

- **其中：必须先将文件提交到暂存区，不能直接提交到版本库**
- 添加到暂存区：`git add .`（. 表示将所有文件提交，add 和 . 之间有空格）
- 添加到版本库：`git commit -m "提交信息（可不写）"`



## 查看历史记录

### 只显示版本号和版本信息

```
git log --oneline
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512132530.png" alt="QQ截图20240512132530" style="zoom:50%;" />



### 显示所有信息

```
git log
```

显示如下：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512132509.png" alt="QQ截图20240512132509" style="zoom:50%;" />



### 显示所有版本（防止回退版本后再回到后面版本）

```
git reflog
```



## 回退历史版本

```
git reset --hard 版本号
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512132740.png" alt="QQ截图20240512132740" style="zoom:80%;" />



## 状态查询

```
git status
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512133515.png" alt="QQ截图20240512133515" style="zoom:50%;" />

+ 红色表示：工作区有文件更改，还没上传到暂存区
+ 绿色表示暂存区有文件更改，还没上传到版本库



# 分支操作

## 查看所有分支

```
 git branch
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512134929.png" alt="QQ截图20240512134929" style="zoom:80%;" />

+ 其中： `*` 表示所处分区



## 创建新分支

```
git barch 分支名
```

+ **注意：创建分支后不会跳转到新分支，需要自己切换分支！**
+ **若需要创建并切换到对应分支，则命令变为：**

```
git checkout -b 新分支名
```

如下图：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512140735.png" alt="QQ截图20240512140735" style="zoom:80%;" />



## 切换分支

```
git checkout 分支名
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512135433.png" alt="QQ截图20240512135433" style="zoom:80%;" />



## 修改分支名

```
git branch -m 旧分支名 新分支名
```



## 删除分支

```
git branch -d 分支名
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512140450.png" alt="QQ截图20240512140450" style="zoom:80%;" />

+ 注意：该命令无法删除没提交的分支，若要强制删除，命令如下：

```
git branch -D 分支名
```



## 合并分支

1. 先切换到目的分支（一般是master）
2. 输入命令

```
git merge 被合并的分支名
```

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512140310.png" alt="QQ截图20240512140310" style="zoom:80%;" />

3. 合并后删除分支



# 推送到远程仓库（gitee为例）

## 1. 先在gitee上创建新仓库

创建完后会有如下提示：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512142546.png" alt="QQ截图20240512142546" style="zoom:50%;" />



## 2. 在本地项目文件夹中关联远程仓库

具体操作如下：

1. 给仓库创建别名

```
git remote add origin 仓库地址
```

地址在上述提示中，或者如下可查看：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512142947.png" alt="QQ截图20240512142947" style="zoom:80%;" />



## 3. 将本地文件推送到远程仓库

### 第一次提交

```
git push -u origin "分支名"
```

### 之后提交

```
git push
```



## 修改关联的远程仓库

1. 先删除原有的远程仓库连接：

```
git remote remove 仓库别名(一般为origin)
```

2. 添加新连接：

```
git remote add origin 仓库地址
```





## 仓库克隆

```
git clone 仓库地址
```

+ 注：克隆仓库会将所有分支克隆过来，而使用`git branch`查看分支时会只显示一个分支，需要使用如下命令查看所有分支

```
git branch -a
```



## 仓库拉取

```
git pull
```


# SSH免密登录

## 1. 生成ssh公钥

在电脑任意位置打开终端输入如下命令：

```
ssh-keygen -t ed25519 -C 公钥名称
```

直接回车3次即可。生成成功后如下图：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512155949.png" alt="QQ截图20240512155949" style="zoom:50%;" />



## 2. 查看及拷贝公钥

```
cat ~/.ssh/id_ed25519.pub
```

复制粘贴所有，输入到gitee，如下：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512160333.png" alt="QQ截图20240512160333" style="zoom:50%;" />





## 测试激活公钥

```
ssh -T git@gitee.com
```

之后会弹出提示，是否继续连接，输入yes即可

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512160608.png" alt="QQ截图20240512160608" style="zoom:80%;" />

之后出现`successfully`，连接成功

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512160659.png" alt="QQ截图20240512160659" style="zoom:80%;" />



之后新建仓库可以直接使用ssh配置

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512161307.png" alt="QQ截图20240512161307" style="zoom: 80%;" />



# .gitignore 忽略文件

## 语法

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512133208.png" alt="QQ截图20240512133208" style="zoom:80%;" />



# VSCode中的git

在源代码管理中，可以提交代码。

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512161938.png" alt="QQ截图20240512161938" style="zoom:50%;" />

当你的项目根目录执行过`git init`后，会变成如下这样：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512162135.png" alt="QQ截图20240512162135" style="zoom:50%;" />

当你修改文件之后可以提交，此处提交等价于`commit`，之后可以再次点击同步更改，此处等效于`push`



# 显示隐藏文件夹

- `win 10`系统中：打开任意文件夹，让后如下操作：

<img src="/md-images/学习笔记/git.assets/QQ%E6%88%AA%E5%9B%BE20240512112931.png" alt="QQ截图20240512112931" style="zoom:50%;" />









