---
title: linux环境下安装与操作mysql
date: 2019-12-11 18:51:15
tags:
- mysql
categories: 
- 教程
---

![1](https://1716416169.github.io/linux环境下安装与操作mysql/1.png)

# 前言

本文用于在linux（Centos7）环境下安装mysql



# 下载

首先，你得创建一个下载mysql的文件夹

	mkdir mysql

然后进到这个文件夹中

	cd /mysql

ok现在来下载（用wget的形式）

	wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm

然后是安装下载的rpm包

	rpm -ivh mysql-community-release-el7-5.noarch.rpm

更新一下yum（如果需要的话）

	yum update

下载安装mysql的服务

	yum install mysql-server

修改mysql的权限

	chown mysql:mysql -R /var/lib/mysql

初始化mysql

	mysqld --initialize

好的一切就绪，启动mysql

	systemctl start mysqld

查看运行状态

	systemctl status mysqld

验证mysql的安装

	mysqladmin --version

如果到这步一切正常，那么现在开始操作mysql进行一些基础的设置

修改登录密码

	mysqladmin -u root password "new_password";

然后以此来登录

	mysql -u root -p