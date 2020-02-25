
---
layout: post
title: docker安装redis
category: docker
tags: [docker]
---

以上场景在CentOS 7.6, Docker安装 redis

## docker安装redis

### 查询镜像

> 搜索出相关镜像

```
docker search redis
```

### 拉取redis镜像
> 拉取Dorcker Hub镜像，如果不注明版本号，则拉取最新版本（此步可省略）

```
docker pull redis
```

### 创建并运行redis容器

> -d   后台运行
  -v   将主机目录挂载到容器的目录
  –name   实例运行后的名字 redis-dev
  -p   容器端口映射到主机的端口
  -requirepass  设置的密码
   redis-server   在容器执行redis-server启动命令，
   --appendonly yes     并打开redis持久化配置

```
docker run -d  -v /docker/redis/data:/data --name redis-dev -p 6379:6379 redis redis-server --requirepass "123456" --appendonly yes 
```

## redis可视化工具连接

> 安装完还需要在云服务器ECS安全组开放7693端口才可访问

![](https://note.youdao.com/yws/public/resource/c69550117149dc587daddc4bb4d7211e/xmlnote/D8D64936275940B0B64ED7B5BDA50792/4358)

> name：随意填写 host：填写自己的ip  ，以下情况成功连接

![](https://note.youdao.com/yws/public/resource/c69550117149dc587daddc4bb4d7211e/xmlnote/16436ABB666E482C855065C631D59FAE/4360)
