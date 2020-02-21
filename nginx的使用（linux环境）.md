---
title: nginx的使用（linux环境）
date: 2019-12-13 20:11:15
tags:
- nginx
categories: 
- 教程
---

![1](https://1716416169.github.io/nginx的使用（linux下）/1.png)



# 前言

nginx是一个高性能的HTTP和反向代理web服务器。本文将介绍它的安装，请求转发和负载均衡配置

# 为什么要使用nginx
nginx可以用来进行负载均衡，还可以进行请求的分发，例如解决如何使用一个域名来完成不同项目的访问（通过url的不同来完成请求的转发），除此之外，还可以解决传递cookie值时因为同源策略（2级域名不同cookie可以传递，但不可以保存）导致的问题，当然以上只是博主遇到的一小部分问题，具体怎么使用还得看你自己了

# 安装编译工具及库文件

首先先安装nginx所需要的编译工具及库文件（yum安装方式）

	yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel

# 安装 PCRE
先创建一个文件夹

	mkdir pcre

然后进入其中

	cd /pcre

下载（wget）

	wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz

解压缩

	tar zxvf pcre-8.35.tar.gz

进入解压缩后的文件中

	cd pcre-8.35

编译安装

	./configure
	make && make install

安装完成后查看pcre版本

	pcre-config --version

# 安装Nginx
先创建一个文件夹

	mkdir nginx

然后进入其中

	cd /nginx

下载（wget）

 	wget http://nginx.org/download/nginx-1.6.2.tar.gz

解压缩

	tar zxvf nginx-1.6.2.tar.gz

进入解压缩的文件内

	cd /nginx-1.6.2

编译安装

	./configure --prefix=/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/pcre-8.35
	make
	make install

查看nginx版本

	nginx -v

至此nginx安装完毕



# Nginx的命令

## nginx启动

	/nginx/sbin/nginx  

## nginx配置文件的重新载入

	/nginx/sbin/nginx -s reload

## nginx停止

	/nginx/sbin/nginx -s stop

## ngin重启

	/nginx/sbin/nginx -s reopen



# nginx对请求的反向代理配置

首先你需要进到nginx的配置文件里去

	cd /nginx/conf

然后修改配置文件的参数

	vim nginx.conf

![2](https://1716416169.github.io/nginx的使用（linux下）/2.png)

你需要修改http字段下的server字段

|  字段名称   | 解释                                                         |
| :---------: | ------------------------------------------------------------ |
|   listen    | nginx要监听的端口，地址。nginx将会对通过该接口的请求进行处理 |
| server_name | 一个变量                                                     |
|  location   | 空格后接你要映射的url ；对其中的字段进行配置，可以有多个     |
| proxy_pass  | 你要转发到的具体路径，可以是相对路径，也可是绝对路径，详见下方的例子 |

> 在nginx中配置proxy_pass代理转发时，如果在proxy_pass后面的url加/，表示绝对根路径；如果没有/，表示相对路径，把匹配的路径部分也给代理走。

假设下面四种情况分别用 http://127.6.6.1/proxy/test.html 进行访问。

第一种：

location /proxy/ {

  proxy_pass http://127.0.0.1/;

}

代理到URL：http://127.0.0.1/test.html

第二种（相对于第一种，最后少一个 / ）

location /proxy/ {

  proxy_pass http://127.0.0.1;

}

代理到URL：http://127.0.0.1/proxy/test.html

第三种：

location /proxy/ {

  proxy_pass http://127.0.0.1/aaa/;

}

代理到URL：http://127.0.0.1/aaa/test.html

第四种（相对于第三种，最后少一个 / ）

location /proxy/ {

  proxy_pass http://127.0.0.1/aaa;

}

代理到URL：http://127.0.0.1/aaatest.html

# 其他

nginx是需要运行在端口的（随意哪个端口）

记住配置nginx监听的端口（否则nginx就没有意义了）

记得启动nginx

echosite别映射错端口了

映射规则别写错
