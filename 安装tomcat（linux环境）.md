---
title: 安装tomcat（linux环境）
date: 2019-12-16 14:20:11
tags:
- tomcat
categories: 
- 教程
---

![1](https://1716416169.github.io/安装tomcat（linux环境）/1.png)

# 前言
Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选，当然，你也可以单纯用来跑纯html的项目（前后端分离）

# 下载tomcat
本人保存在 /tomcat 文件夹内

	mkdir tomcat

这里用wget的方式直接下载到服务器上

	wget https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-9/v9.0.29/bin/apache-tomcat-9.0.29.tar.gz #清华大学开源镜像库，也可以用其他的

# 解压

	 tar -xzvf apache-tomcat-9.0.29.tar.gz

# 修改tomcat的配置文件

	![2](2.pngvim /tomcat/apache-tomcat-9.0.29/conf/server.xml

![2](https://1716416169.github.io/安装tomcat（linux环境）/2.png)

上图为tomcat运行的端口配置，默认8080，但如果有需要可以自行修改

# 运行
将项目丢到webapps文件中，以项目文件名来访问就ok（java是war包名字）

	cd /tomcat/apache-tomcat-9.0.29/bin
	./startup.sh 

# 关闭

	cd /tomcat/apache-tomcat-9.0.29/bin
	./shutdown.sh

# 查看运行状态

	ps -ef|grep xxxxxx