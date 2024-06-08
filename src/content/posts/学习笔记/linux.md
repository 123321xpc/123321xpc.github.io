---
title: linux 学习笔记
published: 2024-05-20
description: ''
image: ''
tags: [linux, 学习笔记]
category: '学习笔记'
draft: false 
---

- [VMware Pro 密钥](#vmware-pro-密钥)
- [Linux系统下载](#linux系统下载)
- [系统安装](#系统安装)
  - [初始安装](#初始安装)
  - [配置网络](#配置网络)
- [快照拍摄(系统还原)](#快照拍摄系统还原)
- [连接xshell与xftp](#连接xshell与xftp)
- [Linux快捷键](#linux快捷键)
  - [光标移动](#光标移动)
  - [剪切](#剪切)
- [命令提示符\[root@localhost ~\]](#命令提示符rootlocalhost-)
- [目录结构](#目录结构)
- [帮助指令](#帮助指令)
  - [help](#help)
  - [--help](#--help)
  - [man](#man)
- [目录操作指令](#目录操作指令)
  - [pwd](#pwd)
  - [cd](#cd)
  - [ls](#ls)
  - [mkdir创建目录](#mkdir创建目录)
  - [rmdir删除目录](#rmdir删除目录)
- [文件操作指令](#文件操作指令)
  - [touch(修改文件时间属性)](#touch修改文件时间属性)
  - [cp(复制文件)](#cp复制文件)
  - [mv(移动剪切指令)](#mv移动剪切指令)
- [文件查看指令](#文件查看指令)
  - [cat](#cat)
  - [more](#more)
  - [less](#less)
  - [head](#head)
  - [tail](#tail)
- [其他指令](#其他指令)
  - [date](#date)
    - [设置时间](#设置时间)
  - [搜索指令](#搜索指令)
    - [find](#find)
    - [grep](#grep)
  - [`>`和`>>`输出重定向指令](#和输出重定向指令)
  - [`|`管道](#管道)
  - [`&&`逻辑控制](#逻辑控制)
- [打包与压缩](#打包与压缩)
  - [gzip格式](#gzip格式)
  - [bzip2格式](#bzip2格式)
- [编辑器](#编辑器)
  - [三种模式](#三种模式)
  - [命令模式下的操作](#命令模式下的操作)
    - [复制和粘贴](#复制和粘贴)
    - [撤销操作](#撤销操作)
  - [命令模式转化为编辑模式](#命令模式转化为编辑模式)
  - [底线命令模式](#底线命令模式)
  - [处理常见错误](#处理常见错误)
  - [服务器突然断开，来不及保存](#服务器突然断开来不及保存)
- [用户和用户组管理](#用户和用户组管理)
  - [useradd添加用户](#useradd添加用户)
  - [passwd设置密码](#passwd设置密码)
  - [usermod修改信息](#usermod修改信息)
  - [userdel删除用户](#userdel删除用户)
  - [id查看用户信息](#id查看用户信息)
  - [groupadd添加用户组](#groupadd添加用户组)
  - [groupmod修改用户组](#groupmod修改用户组)
  - [groupdel删除用户组](#groupdel删除用户组)
  - [查看当前登录用户信息](#查看当前登录用户信息)
  - [su/sudo用户切换](#susudo用户切换)
- [权限管理](#权限管理)
  - [权限设定](#权限设定)
  - [chmod](#chmod)
  - [chown](#chown)
  - [chgrp](#chgrp)
  - [umask权限掩码](#umask权限掩码)
- [磁盘管理](#磁盘管理)
  - [df查看磁盘占用情况](#df查看磁盘占用情况)
  - [du查看文件大小](#du查看文件大小)
- [进程管理](#进程管理)
  - [ps查看进程情况](#ps查看进程情况)
  - [top查看所有进程（实时更新）](#top查看所有进程实时更新)
  - [pstree查看进程（树状）](#pstree查看进程树状)
  - [lsof列出进程调用或打开文件信息](#lsof列出进程调用或打开文件信息)
  - [kill终止进程](#kill终止进程)
- [服务管理](#服务管理)
- [常用命令](#常用命令)
  - [systemctl](#systemctl)
  - [设置开启自启动](#设置开启自启动)
  - [开关机相关](#开关机相关)
  - [关闭防火墙](#关闭防火墙)
- [shell编程](#shell编程)
  - [创建文件](#创建文件)
  - [执行脚本](#执行脚本)
  - [echo](#echo)
    - [read](#read)
    - [显示换行](#显示换行)
    - [将显示结果输入至文件](#将显示结果输入至文件)
  - [变量](#变量)
    - [使用变量](#使用变量)
    - [赋值](#赋值)
    - [删除变量](#删除变量)
  - [字符串](#字符串)
    - [获得字符串长度](#获得字符串长度)
    - [截取子串](#截取子串)
    - [查找子串](#查找子串)
  - [注释](#注释)
  - [数组](#数组)
    - [获取数组长度](#获取数组长度)
  - [参数传递](#参数传递)
  - [运算符](#运算符)
    - [算术运算符](#算术运算符)
    - [关系运算符](#关系运算符)
  - [test](#test)
  - [流程控制](#流程控制)
    - [if](#if)
    - [for](#for)
    - [while](#while)
    - [case](#case)
    - [break \& continue](#break--continue)
    - [函数](#函数)



# VMware Pro 密钥

```
NA20H-0NK40-480Z8-C9C54-A6020
```



# Linux系统下载

```
https://mirrors.tuna.tsinghua.edu.cn/centos-vault/7.6.1810/isos/x86_64/
```

![QQ截图20231220140207](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140207.png)



# 系统安装

## 初始安装

+ 全部默认即可

## 配置网络

- 配置vmware网卡：

![QQ截图20231220140540](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140540.png)

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140626.png" alt="QQ截图20231220140626" style="zoom: 67%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140650.png" alt="QQ截图20231220140650" style="zoom:67%;" />



- 之后在断开虚拟机的前提下，

![QQ截图20231220140843](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140843.png)

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140914.png" alt="QQ截图20231220140914" style="zoom:67%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220140945.png" alt="QQ截图20231220140945" style="zoom:67%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220141019.png" alt="QQ截图20231220141019" style="zoom:67%;" />



- 启动虚拟机
- 输入：`vi /etc/sysconfig/network-scripts/ifcfg-ens33`

![QQ截图20231220143027](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220143027.png)

- 保存



# yum换源

## 手动换源

```
yum install -y wget

#下载新的yum源
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo 

#更新yum缓存
yum clean all 
yum makecache
```



## 自动换源

```
#安装yum-utils
yum -y install yum-utils 

#更改yum源
yum-config-manager --add-repo http://mirrors.aliyun.com/repo/Centos-7.repo 

#更新yum缓存
yum makecache                      
```



## 常见源

```
#CentOS 7 阿里云yum源
http://mirrors.aliyun.com/repo/Centos-7.repo 

#CentOS 7 清华大学yum源
http://mirrors.tuna.tsinghua.edu.cn/help/centos/
```



# 快照拍摄(系统还原)

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220141359.png" alt="QQ截图20231220141359" style="zoom:67%;" />



# 连接xshell与xftp

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220142340.png" alt="QQ截图20231220142340" style="zoom:67%;" />

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220142524.png" alt="QQ截图20231220142524" style="zoom:67%;" />



# Linux快捷键

## 光标移动

![QQ截图20231220143457](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220143457.png)



## 剪切

![QQ截图20231220143555](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220143555.png)



# 命令提示符[root@localhost ~] #

![QQ截图20231220144144](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220144144.png)



# 目录结构

![QQ截图20240123160844](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240123160844.png)



# 帮助指令

## help

<img src="https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220144658.png" alt="QQ截图20231220144658" style="zoom:67%;" />



## --help

![QQ截图20231220144717](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220144717.png)



## man

 ![QQ截图20231220144904](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220144904.png)



# 目录操作指令

## pwd

![QQ截图20231220145303](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220145303.png)



## cd

![QQ截图20231220145703](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220145703.png)



## ls

![QQ截图20231220150100](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220150100.png)



## mkdir创建目录

![QQ截图20231220150509](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220150509.png)



## rmdir删除目录

![QQ截图20231220150853](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220150853.png)



# 文件操作指令

## touch(修改文件时间属性)

![QQ截图20231220150946](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220150946.png)



## cp(复制文件)

![QQ截图20231220151151](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220151151.png)



## mv(移动剪切指令)

![QQ截图20231220151827](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220151827.png)



# 文件查看指令

## cat

![QQ截图20231220151952](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220151952.png)



## more

![QQ截图20231220152231](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220152231.png)



## less

![QQ截图20231220152725](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220152725.png)



## head

![QQ截图20231220153119](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220153119.png)



## tail

![QQ截图20231220153340](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220153340.png)



# 其他指令

## date

![QQ截图20231220153935](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220153935.png)

### 设置时间

![QQ截图20231220154144](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220154144.png)



## 搜索指令

### find

![QQ截图20231220154423](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220154423.png)

- 选项：

![QQ截图20231220154605](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220154605.png)

![QQ截图20231220154705](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220154705.png)

![QQ截图20231220154755](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220154755.png)

- 寻找不是以`txt`结尾的文件

![QQ截图20231220155306](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220155306.png)



### grep

![QQ截图20231220155442](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220155442.png)



## `>`和`>>`输出重定向指令

![QQ截图20231220160626](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220160626.png)



## `|`管道

![QQ截图20231220160946](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220160946.png)



## `&&`逻辑控制

![QQ截图20231220161142](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220161142.png)



# 打包与压缩

![QQ截图20231220161712](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220161712.png)



![QQ截图20231220162055](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220162055.png)



## gzip格式

![QQ截图20231220162406](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220162406.png)



## bzip2格式

![QQ截图20231220162917](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220162917.png)



# 编辑器

![QQ截图20231220163227](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220163227.png)



## 三种模式

![QQ截图20231220163408](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220163408.png)

![QQ截图20231220163423](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220163423.png)



![QQ截图20231220163619](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220163619.png)

![QQ截图20231220163637](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220163637.png)



## 命令模式下的操作

### 复制和粘贴

![QQ截图20231220164008](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220164008.png)

![QQ截图20231220164134](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220164134.png)



### 撤销操作

![QQ截图20231220163953](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220163953.png)



## 命令模式转化为编辑模式

![QQ截图20231220164254](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220164254.png)



## 底线命令模式

![QQ截图20231220164453](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220164453.png)



## 处理常见错误

## 服务器突然断开，来不及保存

![QQ截图20231220165205](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20231220165205.png)

- 恢复：`vim -r 文件名`-



# 用户和用户组管理

![QQ截图20240111172902](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111172902.png)

## useradd添加用户

![QQ截图20240111173132](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111173132.png)

## passwd设置密码

![QQ截图20240111173951](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111173951.png)

![QQ截图20240111174106](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111174106.png)

- **注：只有管理员才能修改其他用户密码！**



##  usermod修改信息

![QQ截图20240111175639](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111175639.png)

 

## userdel删除用户

![QQ截图20240111180307](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111180307.png)



## id查看用户信息

![QQ截图20240111180400](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111180400.png)



## groupadd添加用户组

![QQ截图20240111181014](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111181014.png)



## groupmod修改用户组

![QQ截图20240111181052](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111181052.png)



## groupdel删除用户组

![QQ截图20240111181059](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111181059.png)



## 查看当前登录用户信息

![QQ截图20240111182022](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111182022.png)

![QQ截图20240111182153](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111182153.png)

## su/sudo用户切换

![QQ截图20240111182655](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111182655.png)



![QQ截图20240111183133](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111183133.png)

- 注意：

![QQ截图20240111183444](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111183444.png)



# 权限管理

![QQ截图20240111183824](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111183824.png)

![QQ截图20240111184227](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111184227.png)

![QQ截图20240111184342](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111184342.png)

![QQ截图20240111184407](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111184407.png)

## 权限设定

## chmod

![QQ截图20240111184815](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111184815.png)

![QQ截图20240111184852](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111184852.png)



![QQ截图20240111184938](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111184938.png)

## chown

![QQ截图20240111185853](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111185853.png)



## chgrp

![QQ截图20240111190117](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111190117.png)



## umask权限掩码

![QQ截图20240111190252](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111190252.png)

![QQ截图20240111190338](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111190338.png)

![QQ截图20240111190454](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111190454.png)

![QQ截图20240111190607](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111190607.png)

![QQ截图20240111190645](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240111190645.png)



# 磁盘管理

## df查看磁盘占用情况

![QQ截图20240112152938](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112152938.png)



## du查看文件大小

![QQ截图20240112153107](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112153107.png)



# 进程管理

## ps查看进程情况

![QQ截图20240112153934](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112153934.png)

## top查看所有进程（实时更新）

![QQ截图20240112155413](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112155413.png)

![QQ截图20240112155448](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112155448.png)



## pstree查看进程（树状）

![QQ截图20240112160652](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112160652.png)



## lsof列出进程调用或打开文件信息

![QQ截图20240112161105](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112161105.png)



## kill终止进程

![QQ截图20240112161909](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112161909.png)

![QQ截图20240112161914](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112161914.png)



![QQ截图20240112163003](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112163003.png)

![QQ截图20240112163003](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112163003-17050483674711.png)



# 服务管理

![QQ截图20240112163815](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112163815.png)

# 常用命令

## systemctl

![QQ截图20240112164236](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112164236.png)

![QQ截图20240112164506](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112164506.png)

![QQ截图20240112164711](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112164711.png)

## 设置开启自启动

![QQ截图20240112164740](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112164740.png)

## 开关机相关

![QQ截图20240112164820](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112164820.png)

## 关闭防火墙

![QQ截图20240112164924](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240112164924.png)

# shell编程

## 创建文件

![QQ截图20240113133723](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113133723.png)

## 执行脚本

![QQ截图20240113133754](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113133754.png)



## echo

![QQ截图20240114133748](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114133748.png)

### read

![QQ截图20240114133916](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114133916.png)

`read`是从键盘输入值，并赋给后面的变量。 



### 显示换行

![QQ截图20240114133924](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114133924.png)

### 将显示结果输入至文件

![QQ截图20240114134012](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114134012.png)

- 注：`>`是覆盖原数据，`>>` 是追加至原数据末尾。



## 变量

![QQ截图20240113134522](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113134522.png)

### 使用变量

![QQ截图20240113134634](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113134634.png)

### 赋值

![QQ截图20240113134801](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113134801.png)

![QQ截图20240113134837](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113134837.png)

### 删除变量

![QQ截图20240113140310](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113140310.png)

## 字符串

![QQ截图20240113141951](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113141951.png)

### 获得字符串长度

![QQ截图20240113141630](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113141630.png)

### 截取子串

![QQ截图20240113141649](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113141649.png)

### 查找子串

![QQ截图20240113141832](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113141832.png)

- **下标从1开始找！**



## 注释

![QQ截图20240113143116](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113143116.png)

## 数组

![QQ截图20240113143318](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113143318.png)

### 获取数组长度

![QQ截图20240113143827](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113143827.png)



## 参数传递

![QQ截图20240113143903](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113143903.png)

- 注：`$0`是获取脚本文件名(包含路径)

![QQ截图20240113144239](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240113144239.png)



## 运算符

![QQ截图20240114132544](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114132544.png)

### 算术运算符

![QQ截图20240114132705](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114132705.png)



- 注：`/`结果只取整数部分。即`10 / 20 = 0`



![QQ截图20240114133238](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114133238.png)



### 关系运算符

![QQ截图20240114133500](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114133500.png)

- 注：只支持比较数字！

![QQ截图20240114133717](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114133717.png)



## test

![QQ截图20240114135249](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114135249.png)

![QQ截图20240114135310](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114135310.png)



## 流程控制

### if

![QQ截图20240114135435](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114135435.png)

![QQ截图20240114135533](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114135533.png)

 

### for

![QQ截图20240114142609](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114142609.png)

![QQ截图20240114142710](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114142710.png)

### while

![QQ截图20240114143202](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114143202.png)

### case

![QQ截图20240114143552](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114143552.png)

例：

![QQ截图20240114143801](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114143801.png)



### break & continue

![QQ截图20240114143844](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114143844.png)

![QQ截图20240114143915](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240114143915.png)



### 函数

- 创建函数：

![QQ截图20240118163251](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240118163251.png)



- 调用函数

直接使用函数名即可。

![QQ截图20240118163333](https://vip.123pan.cn/1828962653/md-images/linux.assets/QQ截图20240118163333.png)

- 函数传参：同参数传递！

![image-20240604165815297](https://vip.123pan.cn/1828962653/md-images/linux.assets/image-20240604165815297.png)