---
layout: post
title: linux Docker常见命令
category: docker
tags: [docker]
---

 
# **docker服务**  
 
```systemctl start docker``` 启动 

```systemctl status docker``` 查看docker进程状态 

```sudo systemctl daemon-reload``` 守护进程重启

```systemctl restart docker``` 重启docker服务 

```sudo service docker restart``` 重启docker服务

```service docker stop``` 关闭docker 

```systemctl stop docker``` 关闭docker

```/bin/systemctl stop docker.service``` 关闭docker 

# **镜像**  

```docker images```  列出本地所有镜像

```docker search 镜像名称 ``` 搜索相关镜像

```
docker pull image_name    

docker pull image_name:tag

image_name：表示镜像的仓库源名称,TAG：
镜像的标签 如果不指定tag 那么默认用最新的
``` 
<font color="red">强制删除 如果镜像有容器在运行  那么就需要强制删除 增加 -f 参数</font> 

    docker rmi 镜像名称/镜像ID
    docker rmi -f 镜像名称/镜像ID
    
<font color="red">删除全部的images； 可通过 -f 参数强制删除</font>

    docker rmi $(docker images -q)
        
    docker rmi -f $(docker images -q)



#  **容器**  

```docker ps``` 查看当前正在运行的容器  

```docker ps -a``` 查看当前正在运行的容器
```
docker start 容器ID/容器名称     启动容器
docker restart 容器ID/容器名称   重启容器
```    
    docker stop 容器ID/容器名称     停止容器
    docker stop $(docker ps -a -q)  停止所有的容器

```docker rm $(docker ps -a -q)```删除所有的容器

