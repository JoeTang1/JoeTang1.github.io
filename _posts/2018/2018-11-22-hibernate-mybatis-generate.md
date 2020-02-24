---
layout: post
title: 在Idea中连接数据库并生成实体类（mybatis逆向生成实体类）
category: arch
excerpt: hibernate-mybatis生成实体
---

## 连接数据库

### 1. 按下图 ,点击view-----选择tool windows----------选择database并点击


![image](http://jerrythh.com/assets/images/2018/java/generate1.png)

### 2. 弹出Database窗口

![image](http://jerrythh.com/assets/images/2018/java/generate1.png)

### 3. 弹出DataSources and Drivers窗口
分别填写画圈的方框。

 * host-----写ip地址

 * Database-------写数据库名称

 * user-------写账号

 * Password------写密码
 
填好之后，可以点击一下test Connection,如果连接成功，那么test Connection按钮的右边会显示 一句话提示连接成功。连接成功后就点击右下角的OK。
 
![image](http://jerrythh.com/assets/images/2018/java/generate3.png)

### 4. 点击OK后出现如下结果，Database下出现一个数据库

### 5. 添加hibernate 配置文件

![image](http://jerrythh.com/assets/images/2018/java/generate4.png)

![image](http://jerrythh.com/assets/images/2018/java/generate5.png)

### 6. choose Data Source 

choose Data Source ------------------------点击右边下三角选择数据库

Package----------------------选择项目中的某个包，生成的实体将会变成一个类文件放在那个包下

第三部分显示的是数据库的表，每个表生成一个实体，勾选，想要生成实体的表，然后按右下角OK即可。这样就可以生成实体了。
    
![image](http://jerrythh.com/assets/images/2018/java/generate6.png) 