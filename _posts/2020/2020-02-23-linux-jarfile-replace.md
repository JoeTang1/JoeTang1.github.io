---
layout: post
title: linux_直接在linux里面替换jar包里的某个文件
category: linux
tags: [linux]
---


<font color=red>场景描述：jar包（```eureka-server-1.0.0.jar```）中替换文件```application.properties```的内容</font>

## 查询需要替换的文件在jar中的位置
> jar tvf *****.jar | grep {fileName}
```
jar tvf eureka-server-1.0.0.jar | grep application.properties
```

![](http://jerrythh.com/assets/images/2020/linux/linux-jar1.jpg)

## 将文件解压到当前目录
>jar xvf ****.jar {filePath} 

此命令将文件所在目录解压出来，会在当前目录生成一个新的文件夹，目录结构同：{filePath}



```
jar xvf eureka-server-1.0.0.jar BOOT-INF/classes/application-pro.properties
```

![](http://jerrythh.com/assets/images/2020/linux/linux-jar2.jpg)

![](http://jerrythh.com/assets/images/2020/linux/linux-jar3.jpg
)
  BOOT-INF中即为解压的文件
  
## 进入解压的目录修改文件内容

![](http://jerrythh.com/assets/images/2020/linux/linux-jar4.jpg)  

## 将替换后的目录打包进jar文件 实现替换
>jar uvf ***.jar {filePath}
```
jar uvf eureka-server-1.0.0.jar BOOT-INF/classes/application.properties
```

![](http://jerrythh.com/assets/images/2020/linux/linux-jar5.jpg) 

参考：
<https://blog.csdn.net/luoww1/article/details/90374770>