---
layout: post
title: docker安装rabbitmq
category: docker
tags: [docker]
---

docker上部署启动RabbitMQ（消息队列）

## docker安装RabbitMQ

### 查询镜像

> 搜索出相关镜像

```
docker search rabbitmq
```


### 拉取RabbitMQ镜像
> 拉取Dorcker Hub镜像，如果不注明版本号，则拉取最新版本（此步可省略）

```
docker pull rabbitmq
```

### 创建并运行RabbitMQ容器

```
docker run -d --name myrabbitmq -p 5672:5672 -p 15672:15672 docker.io/rabbitmq:3-management
```

> -d   后台运行
> --name:指定容器名称
>  -p: 容器端口号映射到本地  

*<font color:"red">注：云服务器以下端口都需要开放</font>*

>  15672：rabbitmq web访问服务端口 
>   5672：rabbitmq 程序连接端口
 

## 访问管理界面
http://ip:15672 访问

>   默认账户名：guest   &emsp;   密码：guest

以下情况访问即为成功安装

![](http://jerrythh.com/assets/images/2020/docker/dockerrabbitmq/1.png)
