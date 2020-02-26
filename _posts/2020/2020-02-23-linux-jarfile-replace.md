---
layout: post
title: linux_直接在linux里面替换jar包里的某个文件
category: Linux
tags: [Linux]
---


<font color=red>场景描述：jar包（```eureka-server-1.0.0.jar```）中替换文件```application.properties```的内容</font>

## 查询需要替换的文件在jar中的位置
> jar tvf *****.jar | grep {fileName}
```
jar tvf eureka-server-1.0.0.jar | grep application.properties
```

![](https://note.youdao.com/yws/public/resource/23c043803be080a153110dced7dbfc97/xmlnote/060295EA23614B69B5D74C06DD0C7411/4114)

## 将文件解压到当前目录
>jar xvf ****.jar {filePath} 

此命令将文件所在目录解压出来，会在当前目录生成一个新的文件夹，目录结构同：{filePath}



```
jar xvf eureka-server-1.0.0.jar BOOT-INF/classes/application-pro.properties
```

![](https://note.youdao.com/yws/public/resource/23c043803be080a153110dced7dbfc97/xmlnote/E753489A632846FAAF19BA3C10199F5D/4116)

![](https://note.youdao.com/yws/public/resource/23c043803be080a153110dced7dbfc97/xmlnote/A06DF47992EF416D8A52201B106CF69F/4112
)
  BOOT-INF中即为解压的文件
  
## 进入解压的目录修改文件内容

![](https://note.youdao.com/yws/public/resource/23c043803be080a153110dced7dbfc97/xmlnote/D8F76798BBA74481BE6EDB9128FA8FE1/4113)  

## 将替换后的目录打包进jar文件 实现替换
>jar uvf ***.jar {filePath}
```
jar uvf eureka-server-1.0.0.jar BOOT-INF/classes/application.properties
```

![](https://note.youdao.com/yws/public/resource/23c043803be080a153110dced7dbfc97/xmlnote/4379F2ABFE124ED988292A0B126BF3AE/4115) 

参考：
<https://blog.csdn.net/luoww1/article/details/90374770>