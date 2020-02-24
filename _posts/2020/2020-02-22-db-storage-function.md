---
layout: post
title: 数据库中存储过程和函数的区别
category: DB
tags: [db]
---

转载：[https://www.cnblogs.com/zhycyq/articles/2454758.html](https://www.cnblogs.com/zhycyq/articles/2454758.html)

## **数据库中存储过程和函数的区别**

**函数**限制比较多，如:不能用临时表，只能用表变量等，而**存储过程**的限制相对就比较少。

1.一般来说，存储过程实现的功能要复杂一点，而函数的实现的功能针对性比较强。

2.对于存储过程来说可以返回参数，而函数只能返回值或者表对象。

3.存储过程一般是作为一个独立的部分来执行，而函数可以作为查询语句的一个部分来调用，由于函数可以返回一个表对象，因此它可以在查询语句中位于FROM关键字的后面。

4.当存储过程和函数被执行的时候，SQLManager会到procedurecache中去取相应的查询语句，如果在procedurecache里没有相应的查询语句，SQLManager就会对存储过程和函数进行编译。

Procedurecache：中保存的是执行计划，当编译好之后就执行procedurecache中的executionplan，之后SQLSERVER会根据每个executionplan的实际情况来考虑是否要在cache中保存这个plan，评判的标准一个是这个executionplan可能被使用的频率；其次是生成这个plan的代价，也就是编译的耗时。保存在cache中的plan在下次执行时就不用再编译了。

## **存储过程和函数具体的区别：**

存储过程：可以使得对的管理、以及显示关于及其用户信息的工作容易得多。存储过程是SQL语句和可选控制流语句的预编译集合，以一个名称存储并作为一个单元处理。存储过程存储在数据库内，可由应用程序通过一个调用执行，而且允许用户声明变量、有条件执行以及其它强大的编程功能。存储过程可包含程序流、逻辑以及对数据库的查询。它们可以接受参数、输出参数、返回单个或多个结果集以及返回值。

可以出于任何使用SQL语句的目的来使用存储过程，它具有以下优点：

(1)功能强大，限制少。

(2)可以在单个存储过程中执行一系列SQL语句。

(3)可以从自己的存储过程内引用其它存储过程，这可以简化一系列复杂语句。

(4)存储过程在创建时即在上进行编译，所以执行起来比单个SQL语句快。

(5)可以有多个返回值，即多个输出参数，并且可以使用SELECT返回结果集。

函数：是由一个或多个SQL语句组成的子程序，可用于封装代码以便重新使用。自定义函数诸多限制，有许多语句不能使用，许多功能不能实现。函数可以直接引用返回值，用表变量返回记录集。但是，用户定义函数不能用于执行一组修改全局数据库状态的操作