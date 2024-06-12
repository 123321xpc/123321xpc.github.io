---
title: redis
published: 2024-06-08
description: ''
image: ''
tags: [学习笔记, redis]
category: '学习笔记'
draft: false 
---

- [NoSQL](#nosql)
- [安装redis](#安装redis)
	- [windows](#windows)
	- [linux](#linux)
- [常见命令](#常见命令)
	- [KEY：模糊查询（不建议生产环境使用）](#key模糊查询不建议生产环境使用)
	- [DEL：删除](#del删除)
	- [EXIST：判断KEY是否存在](#exist判断key是否存在)
	- [EXPIRE：给KEY设置有效期（秒为单位）](#expire给key设置有效期秒为单位)
	- [TTL：查看KEY的剩余有效期](#ttl查看key的剩余有效期)
- [String类型](#string类型)
	- [set \& get](#set--get)
	- [MSET \& MGET](#mset--mget)
	- [INCR](#incr)
	- [INCRBYFLOAT](#incrbyfloat)
	- [SETNX](#setnx)
	- [SETEX](#setex)
- [Hash类型](#hash类型)
	- [HSET \& HGET](#hset--hget)
	- [HMSET \& HMGET](#hmset--hmget)
	- [HGETALL](#hgetall)
	- [HKEYS \& HVALS](#hkeys--hvals)
	- [List类型](#list类型)
	- [LPUSH \& RPUSH](#lpush--rpush)
	- [LPOP \& RPOP](#lpop--rpop)
- [Set类型](#set类型)
	- [集合操作](#集合操作)
- [KEY的格式](#key的格式)



# NoSQL

![image-20240608195716078](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240608195716078.png)



![image-20240608200251698](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240608200251698.png)



# 安装redis

## windows

- github：`https://github.com/MicrosoftArchive/redis/releases`

- 下载完后添加环境变量（添加redis根目录即可）



## linux

- http://download.redis.io/releases/

- 安装环境

```
yum install -y gcc tcl
```

- 解压后进入目录，执行编译安装命令

```
make && make install
```

- 修改配置文件

```
# 监听的地址，默认是127.0.0.1，会导致只能在本地访问。修改为0.0.0.0则回以在任意ip访问，生产环境不要设置为0.0.0.0
bind 0.0.0.0

# 守护进程，修改为yes后即阿后台运行
daemonize yes

# 密码，设置后访问Redis必须输入密码
requirepass 123321



# 其他可选配置

#监听的端口
port 6379

#工作目录，默认是当前目录，也就是运redis-server时的命令，日志、持久化等文件会保存在这个目录
dir.

#数据库数量，设置为1，代表只使用1个库，认有16个库，编号0~15
databases 1

#设置redis能够使用的最大内存
maxmemory 512mb

#日志文件，默认为空不记录日志，可以指定日志文件名（默认生成在运行redis启动指令的目录）
logfile "redis.log"
```

- 启动与开机自启

	1. 创建`/etc/systemd/system/redis.service`文件
	2. 输入如下内容：

	```
	[Unit]
	Description=redis-server
	After=network.target
	[Service]
	Type=forking
	ExecStart=/usr/local/bin/redis-server /root/redis/redis.conf
	ExecStop=/usr/local/bin/redis-cli -h 127.0.0.1 -p 6379 shutdown
	PrivateTmp=true
	[Install]
	WantedBy=multi-user.target
	```

	3. 加载文件并重启redis

	```
	systemctl daemon-reload
	
	systemctl start redis
	
	systemctl enable redis
	```

	

# 常见命令

## KEY：模糊查询（不建议生产环境使用）

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610160806518.png" alt="image-20240610160806518" style="zoom:67%;" />



## DEL：删除

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610160633321.png" alt="image-20240610160633321" style="zoom:50%;" />



## EXIST：判断KEY是否存在

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610160930092.png" alt="image-20240610160930092" style="zoom: 67%;" />



## EXPIRE：给KEY设置有效期（秒为单位）

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161037800.png" alt="image-20240610161037800" style="zoom:50%;" />

> 注：永久有效，有效期为`-1`



## TTL：查看KEY的剩余有效期

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161152085.png" alt="image-20240610161152085" style="zoom:67%;" />



# String类型

![image-20240610161349879](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161349879.png)

 

## set & get

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161444547.png" alt="image-20240610161444547" style="zoom: 67%;" />



## MSET & MGET

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161522656.png" alt="image-20240610161522656" style="zoom:67%;" />



## INCR

![image-20240610161627622](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161627622.png)



## INCRBYFLOAT

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161734603.png" alt="image-20240610161734603" style="zoom: 67%;" />



## SETNX

 <img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610161913578.png" alt="image-20240610161913578" style="zoom:67%;" />



## SETEX

 ![image-20240610162023745](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610162023745.png)



# Hash类型

![image-20240610162700970](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610162700970.png)



## HSET & HGET

![image-20240610162811118](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610162811118.png)

![image-20240610162949002](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610162949002.png)

> 注：可以使用同样格式对值进行修改。



## HMSET & HMGET

![image-20240610163024969](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163024969.png)



## HGETALL

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163100937.png" alt="image-20240610163100937" style="zoom:67%;" />



## HKEYS & HVALS

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163145125.png" alt="image-20240610163145125" style="zoom:67%;" />



## List类型

![image-20240610163428672](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163428672.png)



## LPUSH & RPUSH

<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163739648.png" alt="image-20240610163739648" style="zoom:67%;" />



<img src="https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163720734.png" alt="image-20240610163720734" style="zoom:50%;" />



## LPOP & RPOP

![image-20240610163839089](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610163839089.png)



> LPOP和RPOP不但会获取到值，还会在表中删除。



# Set类型

![image-20240610164234491](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610164234491.png)



![image-20240610164322543](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610164322543.png)

 

## 集合操作

![image-20240610164428877](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610164428877.png)







# KEY的格式

![image-20240610162514001](https://vip.123pan.cn/1828962653/md-images/redis.assets/image-20240610162514001.png)
