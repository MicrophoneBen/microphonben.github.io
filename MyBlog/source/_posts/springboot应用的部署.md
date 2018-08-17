---
title: springboot应用的部署
date: 2018-08-16 02:08:26
tags: 
	- springboot部署
	- springboot
categories: springboot使用
description: 对写好的springboot应用进行打包发布，遇到的issue
---
# SpringBoot应用的打包发布

接到同事的通知，说要把之前写好的应用打包发布到公司的服务器上，以便用户使用。可是按照常规的步骤执行之后一直有问题，在这里做记录，以后有需要使用的朋友可以借鉴。

## 环境

- CentOs7.3及以上的Linux服务器
- springboot应用，这里使用maven管理
- jdk默认使用1.8及以上
- IntellJ Idea 2018.2 

## 限制

> The default script supports most Linux distributions and is tested on CentOS and Ubuntu. Other platforms, such as OS X and FreeBSD, will require the use of a custom embeddedLaunchScript.
当前文档适用于 CentOS and Ubuntu，其他平台需要定制脚本。详细参见[springboot官方文档](https://docs.spring.io/spring-boot/docs/2.1.0.BUILD-SNAPSHOT/reference/htmlsingle/#deployment-service)

## 步骤及方法


### 添加maven打包依赖

> 我们这里演示的是使用maven作为项目依赖管理，如果使用其他项目依赖管理工具的，参见[springboot官方文档]([springboot官方文档](https://docs.spring.io/spring-boot/docs/2.1.0.BUILD-SNAPSHOT/reference/htmlsingle/#deployment-service))
> 在maven的打包插件，添加依赖

```xml
<plugin>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-maven-plugin</artifactId>
	<configuration>
		<executable>true</executable>
	</configuration>
</plugin>
```

### 打包应用

- 这里演示的是使用idea进行项目打包

![项目打包](http://pdfbk5gmm.bkt.clouddn.com/maven%E5%B7%A5%E7%A8%8B%E6%89%93%E5%8C%85.jpg)

### 应用转移到服务器端

- 使用ftp服务器拉取，或者直接托管到github再拉下来，方法很多，这里不再详述

![拉取成功](http://pdfbk5gmm.bkt.clouddn.com/20180816-033313-003.jpg)

- 拉取到本地服务器之后，要进行测试运行，然后再进行部署
> 我这里把文件拉取到了Share目录下，我是这样测试的


### 应用服务器端测试

1. 首先确定服务器上安装的是jdk1.8,与我们的开发环境相对应就好了

```shell
java -version
```

![jdk版本](http://pdfbk5gmm.bkt.clouddn.com/20180816-032618-002.jpg)

2. 对打包好的应用进行测试。

```shell
#根据官方文档，我们可以使用两种命令,这里的前提是都是在应用jar包的目录下
1 ./yourApplication.jar
2 java -jar yourApplication.jar
```

3. 如果项目有使用数据库，要先进行数据库的安装配置，然后建立项目所需要的数据库以及数据表
4. 然后就是测试运行

![测试截图](http://pdfbk5gmm.bkt.clouddn.com/20180816-033636-004.jpg)
![测试截图2](http://pdfbk5gmm.bkt.clouddn.com/20180816-033707-005.jpg)

5. 不能关闭终端，在浏览器输入你的项目运行端口测试。注意**关闭服务器的防火墙，或者开放端口**

![配置防火墙](http://pdfbk5gmm.bkt.clouddn.com/20180816-040606-008.jpg)

6. 测试成功了再进行下一步的部署安装

### 部署安装

这里分两步。

1. 首先把你的应用打包移动到var目录下

```shell
sudo mv yourApplication.jar /var/
#这里有可能要给文件赋予权限，最好还是加上，不然出错了，你根本不知道都什么原因
chown -R * yourApplication.jar

#切换到var目录查看文件
cd /var
ll
#这里会显示你的应用以及其他文件
……
```

![打包移动](http://pdfbk5gmm.bkt.clouddn.com/store%20to%20var.png)

2. 建立一个软链接，让我们可以使用它，甚至开机启动

![建立链接](http://pdfbk5gmm.bkt.clouddn.com/link%20to%20etc.png)

```shell
ln -s /var/yourApplication.jar /etc/init.d/yourApp

#建立好了软链接之后我们可以试一下系统有没有收录
service yourApp start

#失败会有很多报错的log输出，成功的话，在Centos会有提示，在Ubuntu16.04没有提示

ss -lntup|grep 8899           (查看一下应用端口是否已经监听)
```

![成功部署](http://pdfbk5gmm.bkt.clouddn.com/20180816-035345-006.jpg)
![关闭应用](http://pdfbk5gmm.bkt.clouddn.com/20180816-035417-007.jpg)

### 配置开机启动
- 添加服务开机自启

```shell
chkconfig --add yourApp
```

- 查看一下是否添加成功

```shell
chkconfig --list         （此时yourApp服务应该已经在列表中）
 
service yourApp stop         (手动停止服务)
 
reboot                     （重启服务器）
```

重启服务器后，在查看一下应用端口，或者使用  jps命令， 如果看到你的应用名字，说明配置的
spring boot应用开机自启成功 ， 应用输出控制台日志在   /var/log/yourApp.log  文件中。

## 完成应用部署，记录一下几个坑

1. 检查**jdk的版本**很重要，一定要与你的开发环境一致
2. 注意，当你使用自己安装的jdk时候，要把她链接到系统的一个执行路径上，否则会报 java not found
 > 可以把他链接到 /usr/local/bin目录下
 > 这是系统运行的路径之一

3. 数据库一点要配置正确，否则根本就没有办法运行应用
4. 小心不要两次启动，会出现端口占用的情况。这时候要先停止，再启动. 


































