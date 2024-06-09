---
title: docker 学习笔记
published: 2024-06-08
description: ''
image: ''
tags: [学习笔记, docker]
category: '学习笔记'
draft: false 
---





# 安装

1. 安装需要的软件包

```
yum install -y yum-utils
```



2. 设置`yum`源

```
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

yum makecache fast
```



3. 可以查看所有仓库中所有docker版本，并选择特定版本安装

```
yum list docker-ce --showduplicates | sort -r
```



4. 下载并安装docker

```
 # 这是指定版本安装
yum install -y docker-ce-3:19.03.9-3.el7.x86_64
```



5. 启动并加入开机启动

```
systemctl start docker && systemctl enable docker
```



6. 查看docker版本

```
docker version
```



## 配置阿里云镜像加速(CentOS)

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://kvr5igu6.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```





# 部署Mysql

```
docker run -d --name mysql -p3306:3306 -e TZ=Asia/Shanghai -e MYSQL_ROOT_PASSWORD=123 mysql
```



## 命令解读

![image-20240608151011397](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608151011397.png)

1. `-d`：使程序在后台运行
2. `-p 3306:3306`：设置端口映射：将主机的3306端口映射到mysql的3306端口（前面的是主机端口，可以变，后面是程序端口，不能变）。若运行2个mysql程序，则第二个可改为`-p 3307:3306`



# 常见命令

![image-20240608151500717](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608151500717.png)



## 打包镜像

```
docker save -o 文件名.tar nginx:latest
```



## 从压缩包中加载镜像

```
docker load -i nginx.tar
```



## 删除镜像

```
docker rmi nginx:latest
```



## 查看本地镜像

```
docker images
```



## 查看所有镜像详细信息(默认查看运行中的)

```
docker ps
```

> 若要查看停止状态的容器，在后面加 -a



### 使用命令别名显示固定格式

- 进入文件`vi ~/.bashrc`，添加如下别名

```
alias dps='docker ps --format "table {{.ID}}\\t{{.Image}}\\t{{.Status}}\\t{{.Names}}\\t{{.Ports}}"'
```

- 保存退出后，输入`source ~/.bashrc`使文件生效。



## 启动容器

```
docker start mysql
```



## 停止容器

```
docker stop mysql
```



## 进入容器内部

```
docker exec -it nginx bash
```



## 删除容器（不能删除运行中的容器）

```
docker rm mysql
```



## 拉取容器

```
docker pull nginx:latest
```



## 查看部署日志

```
docker logs -f 容器名
```





# 数据卷

![image-20240608154843509](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608154843509.png)



## 常用命令

![image-20240608154858521](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608154858521.png)

![image-20240608155009632](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608155009632.png)

- 例：挂载`nginx`下的`/usr/share/nginx/html`目录

```
docker run -d --name nginx -p 80:80 -v test:/usr/share/nginx/html nginx
```

- 挂载点查看：`docker volume inspect mystatic`，如下`Mountpoint`即为挂载点

```json
[
    {
        "CreatedAt": "2024-06-08T15:56:43+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mystatic/_data",
        "Name": "mystatic",
        "Options": null,
        "Scope": "local"
    }
]
```



## 查看容器是否有挂载点

- `docker inspect mysql`



## 自定义本地目录挂载

![image-20240608161100764](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608161100764.png)

- 本地目录必须使用`/`或`./`开头，分别表示本地路径和相对路径

```
例如：
在根目录的test目录中挂载：
docker run -d --name nginx -p 80:80 -v /test:/usr/share/nginx/html nginx

在当前目录的test目录中挂载：
docker run -d --name nginx -p 80:80 -v ./test:/usr/share/nginx/html nginx
```



> 注意：这种方法挂载无法在`docker volume ls ` 命令中查到挂载目录，但是可以用`docker inspect nginx` 命令找到。 



# 自定义镜像

##  Dockerfile

![image-20240608175324662](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608175324662.png)



![image-20240608175813953](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608175813953.png)



# 自定义网络

![image-20240608180727170](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608180727170.png)



## 将容器连接到自定义网络

### 方法一：容器已存在

1. 创建网络：

```
docker network create 网络名
```

2. 连接容器

```
docker network connect 网络名 容器名
```



### 方法二：创建容器时连接：

```
docker run -d --network 网络名
```



# DockerCompose

![image-20240608182830529](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608182830529.png)



![image-20240608182918476](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608182918476.png)



## 命令

![image-20240608183314171](https://vip.123pan.cn/1828962653/md-images/docker.assets/image-20240608183314171.png)



