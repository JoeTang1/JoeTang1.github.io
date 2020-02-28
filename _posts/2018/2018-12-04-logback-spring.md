---
layout: post
title: Springboot 日志管理配置logback-spring.xml
category: springboot
excerpt: logback-spring日志
---

## 几种常见的日志
 1. Log4j：是最早的日志框架，是apach旗下的，可以单独使用，也可配合日志框架JCL使用；
 2. Log4j2：apach旗下的关于log4j的升级版；
 3. Logback：是基于slf4j接口实现的一套日志框架组件；（Logback是由log4j创始人设计的又一个开源日志组件。）
 4. JUL(java utillog)：仿log4j实现的日志框架，是sun旗下的，(也就是在我们普遍使用的jdk中)；
 5. Commons loggin：是一套日志接口（apache）；
 6. Slf4j：也是一套日志接口；
 
　   Commons Logging和Slf4j是日志门面(门面模式是软件工程中常用的一种软件设计模式，也被称为正面模式、外观模式。它为子系统中的一组接口提供一个统一的高层接          口，使          得子系统更容易使用)。log4j和Logback则是具体的日志实现方案。可以简单的理解为接口与接口的实现，调用这只需要关注接口而无需关注具体的实现，做到解耦；
 
　　 比较常用的组合使用方式是Slf4j与Logback组合使用，Commons Logging与Log4j组合使用。
    
> 下面是Slf4j与Logback使用
     
## Springboot 日志管理配置logback-spring.xml
 
![image](http://jerrythh.com/assets/images/2018/java/logback1.png)

### （1）application.yml配置

```
 # 日志目录
 logging:
   path: home/logs/
   file: ${logging.path}springboot

```

### （2）logback-spring.xml配置

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- 日志级别从低到高分为TRACE < DEBUG < INFO < WARN < ERROR < FATAL，如果设置为WARN，则低于WARN的信息都不会输出 -->
<!-- scan:当此属性设置为true时，配置文档如果发生改变，将会被重新加载，默认值为true -->
<!-- scanPeriod:设置监测配置文档是否有修改的时间间隔，如果没有给出时间单位，默认单位是毫秒。
                 当scan为true时，此属性生效。默认的时间间隔为1分钟。 -->
<!-- debug:当此属性设置为true时，将打印出logback内部日志信息，实时查看logback运行状态。默认值为false。 -->

<configuration debug="true">
    <!-- name的值是变量的名称，value的值时变量定义的值。通过定义的值会被插入到logger上下文中。定义后，可以使“${}”来使用变量。 -->
    <!--<property name="LOG_FILE" value="${LOG_FILE:-${LOG_PATH:-${LOG_TEMP:-${java.io.tmpdir:-/tmp}}/}spring.log}"/>-->
    <property name="LOG_FILE" value="${LOG_FILE}"/>

    <!--1. 输出到控制台-->
    <appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} %-5level %logger{36} [%line] - %msg%n</pattern>
        </encoder>
    </appender>

    <!--2. 输出到文档-->
    <!-- 2.1 level为 DEBUG 日志，时间滚动输出  -->
    <appender name="R" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 正在记录的日志文档的路径及文档名 -->
        <!--<File>${LOG_FILE}</File>-->
        <!--日志文档输出格式-->
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} %-5level %logger{36} [%line] - %msg%n</pattern>
        </encoder>
        <!-- 日志记录器的滚动策略，按日期，按大小记录 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_FILE}.%d{yyyy-MM-dd}.log
            </fileNamePattern>
            <maxHistory>15</maxHistory>
        </rollingPolicy>
    </appender>

    <logger name="noModule" level="info"/>
    <logger name="org.codehaus" level="info"/>
    <logger name="org.apache" level="info"/>
    <logger name="org.springframework" level="info"/>
    <logger name="druid.sql" level="info"/>
    <logger name="com.alibaba" level="debug">
        <appender-ref ref="stdout"/>
    </logger>
    <logger name="com.springboot" level="debug"/>
    <root level="info">
        <appender-ref ref="stdout"/>
        <appender-ref ref="R"/>
    </root>
</configuration>
```

### （3）生成日志
 
![image](http://jerrythh.com/assets/images/2018/java/logback2.png)

## Slf4j使用
```
(1) public final class InStockController {
     private static final Logger LOGGER = LoggerFactory.getLogger(InStockController.class);
 }

(2)  方法中
  LOGGER.info("xxxxxxxx");

```