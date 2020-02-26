---
layout: post
title: Docker部署springboot，从简单Eureka开始
category: docker
tags: [docker]
---

## 前言

 > docker构建镜像，部署springboot项目已不是新鲜事，就因为docker的持续集成、版本控制、可移植性、隔离性和安全性等优点，使得被大家广泛应用。
今天就分享下自己简单部署Eureka的过程。

## 项目打包

本文前提将简单的Eureka项目利用Maven打成jar包（```eureka-server-1.0.0.jar```）；由于Docker安装在阿里云，所以将打好的jar放在云服务器上（新建个文件夹```/usr/local/dev/docker/testProject/```），
具体打包过程网上有很多分享，不在此细讲。

## Dockerfile

### Dockerfile是什么

> Dockerfile是用来构建Docker镜像的构建文件，是由一系列命令和参数构成的脚本。

####  构建镜像三步骤

   1、 **编写Dockerfile文件**

- 编写的Dockerfile文件和eureka-server-1.0.0.jar放在同级目录下

![](http://jerrythh.com/assets/images/2020/docker/dockerfile/1.png)
    
- Dockerfile配置文件的内容

```    

FROM java:8
VOLUME /tmp
ADD eureka-server-1.0.0.jar /eureka-server.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/eureka-server.jar"]

```  

> - java:8 是使用jdk版本
> - VOLUME 配置数据卷
> -  ADD 将文件拷贝到镜像中并解压，```eureka-server-1.0.0.jar``` 我们打好的jar包，```eureka-server.jar```自定义的镜像容器名称
> -  ENTRYPOINT 容器启动时候执行的命令


   2、**执行Docker构建镜像**

<font color="red">注意后面有个 .</font>

```
 docker build -t eureka-server . 
 ```

> - -t 指定新镜像名eureka-server
> - .  表示Dockfile在当前路径

![](http://jerrythh.com/assets/images/2020/docker/dockerfile/2.png)
创建完镜像后，此时Docker中已经存在eureka-server镜像。

   3、**运行刚才构建成的镜像**

```
docker run -d -p 1001:1001 --name eureka-server eureka-server
```

> - -d 后台运行
>  - -p jar包用的1001端口，主机映射1001端口，容器端口为1001
>  - --name:指定容器名称 

![](http://jerrythh.com/assets/images/2020/docker/dockerfile/3.png)

通过```docker ps```查看此时容器已经运行

## **浏览器访问**

> http:ip + 1001 eureka成功启动

![](http://jerrythh.com/assets/images/2020/docker/dockerfile/4.png)

## 参考
<https://www.cnblogs.com/miller-zou/p/11111756.html>
https://www.cnblogs.com/spll/p/10059542.html

     
     
















 
