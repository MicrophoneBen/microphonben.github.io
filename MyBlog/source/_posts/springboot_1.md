---
title: SpringBoot系列springboot_1
---

# 一、Spring Boot 入门

```java
public static void main (String [] args){
    System.out.println("Hello World");
}
```

## 1、Spring Boot 简介

> 简化Spring应用开发的一个框架；
>
> 整个Spring技术栈的一个大整合；
>
> J2EE开发的一站式解决方案；

## 2、微服务

2014，由martin fowler提出

微服务：架构风格（服务微化）

一个应用应该是一组小型服务；可以通过HTTP的方式进行互通；

单体应用：ALL IN ONE

微服务：每一个功能元素最终都是一个可独立替换和独立升级的软件单元；

[详细参照微服务文档](https://martinfowler.com/articles/microservices.html#MicroservicesAndSoa)

## 3、环境准备

环境约束

- jdk1.8：Spring Boot 推荐jdk1.7及以上；java version "1.8.0_172"

- maven3.x：maven 3.3以上版本；Apache Maven 3.5.4

- IntelliJ IDEA 2018.2 (Ultimate Edition)
Build #IU-182.3684.101, built on July 24, 2018
JRE: 1.8.0_152-release-1248-b8 amd64
JVM: OpenJDK 64-Bit Server VM by JetBrains s.r.o
Windows 10 10.0

- SpringBoot 2.0.0.RELEASE：2.0.0；

统一环境；
