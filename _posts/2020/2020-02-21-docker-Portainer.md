---
layout: post
title: Docker搭建Portainer可视化界面
category: docker
tags: [docker]
---
## 前言
当Docker装有太多容器的时候，有个可视化工具很重要，大大提高的管理Docker的效率。
下面分享下Portainer的简单使用：

## Portainer
> Portainer是Docker的图形化管理工具，提供状态显示面板、应用模板快速部署、容器镜像网络数据卷的基本操作（包括上传下载镜像，创建容器等操作）、事件日志显示、容器控制台操作、Swarm集群和服务等集中管理和操作、登录用户管理和控制等功能。功能十分全面，基本能满足中小型单位对容器管理的全部需求。

## 下载Portainer镜像
### 查询当前有哪些Portainer镜像

```
docker search portainer
```
![](http://jerrythh.com/assets/images/2020/docker/dockerportainer/1.jpg)

上图就是查询出来的有下载量的portainer镜像，我们下载第一个镜像：portainer/portainer。

### 下载Portainer镜像

```
docker pull portainer/portainer
```
 

## 单机版运行
> 如果仅有一个docker宿主机，则可使用单机版运行，Portainer单机版运行十分简单，只需要一条语句即可启动容器，来管理该机器上的docker镜像、容器等数据。

```
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
```

-  -d 后台运行
-  -p 容器端口映射到主机的端口
-  --name:指定容器名称
-  -v 将主机目录挂载到容器的目录

访问方式：http://IP:9000
   - 首次登陆需要注册用户，给admin用户设置密码：XXX ,设置完密码，点击Create user；
   - 单机版这里选择local即可，选择完毕，点击Connect即可连接到本地docker：
![](http://jerrythh.com/assets/images/2020/docker/dockerportainer/2.jpg)

<font color="red">注意：该页面上有提示需要挂载本地 /var/run/docker.socker与容器内的/var/run/docker.socker连接。因此，在启动时必须指定该挂载文件。</font>

容器列表：
![](http://jerrythh.com/assets/images/2020/docker/dockerportainer/3.jpg)

Portainer的一些功能，可以安装上进行了解学习。

## 集群运行（待亲自操作）
>更多的情况下，我们会有一个docker集群，可能有几台机器，也可能有几十台机器，因此，进行集群管理就十分重要了，Portainer也支持集群管理，Portainer可以和Swarm一起来进行集群管理操作。这里我首先搭建了一个Swarm。

Swarm集群的搭建方法可参考这篇文章：通过Swarm搭建Docker集群。<http://www.linuxidc.com/Linux/2017-12/149579.htm>

portainer集群方式启动（这里我喜欢通过简单启动的方式，然后在界面上进行节点的添加）：

```
docker run -d -p 9000:9000 --restart=always --name prtainer-test portainer/portainer
```

启动Portainer之后，首页还是给admin用户设置密码（这里和单机启动一样）。接下来是设置节点了，如下图：
![](https://www.linuxidc.com/upload/2017_12/1712181432337912.png)

这里我们选择Remote这个模块，下面会要求添加一个名字以及节点URL，名字可以自取，只要能够理解即可，Endpoint URL是Swarm集群中设置的节点URL，比如我机器IP是10.0.11.152，监听的端口是默认的2375，则这里的URL就写：10.0.11.152:2375。

如果是集群方式启动，建议portainer安装启动在Swarm管理节点，并且首次设置Endpoint URL时设置管理节点的URL。

填写完毕点击Connect即可进入管理页面。在管理页面左上角会显示管理的集群节点列表：

![](https://www.linuxidc.com/upload/2017_12/1712181432337913.png)

想要查看那个节点的信息，则点击节点即可。镜像、容器操作与单机模式下基本一样。这里只需要说下节点添加。

点击导航栏Endpoints进入节点列表页面：

![](https://www.linuxidc.com/upload/2017_12/1712181432337914.png)

从上图中一目了然就应该知道如何添加节点了，需要填写一个名字Name、Endpoint URL以及节点IP，就可以添加一个集群节点了，十分简单。

OK，Portainer的基本操作就这么多，具体的操作步骤还需要大家自己去学习理解。


## 参考
<https://portainer.readthedocs.io/en/stable/deployment.html>
<https://www.linuxidc.com/Linux/2017-12/149580.htm>
