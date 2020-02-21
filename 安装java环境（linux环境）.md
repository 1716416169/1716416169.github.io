---
title: 安装java环境（linux环境）
date: 2019-12-15 10:33:12
tags:
- java
categories: 
- 教程
---

![1](https://1716416169.github.io/安装java环境（linux环境）/1.png)

# 前言
Java是一门面向对象编程语言，可以编写桌面应用程序、Web应用程序、分布式系统和嵌入式系统应用程序等，是使用排行榜上的常年第一（或者第二），而要想在服务器上运行java程序则需要java的环境（jdk和jvm）。本文内容为在linux环境下完成java环境的安装和配置

# 下载jdk
这里建议去官网下载 [点击这里](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)（需要登录，以前不用，怀念一下sun公司），这里也有准备好的1.8版本。
 [java-jdk.tar.gz](https://1716416169.github.io/安装java环境（linux环境）/java-jdk.tar.gz) 
或者用wget直接下载

	wget xxxxxxx

## 上传到服务器（如果用了wget则直接跳过）
上传工具自选，不管是cmder，还是finalshell（一个国人做的软件，挺好用的），能上传就ok

# 解压压缩包
这里我保存的文件夹是 /java

	cd /java
	tar -zxvf java-jdk.tar.gz 


# 修改配置文件（环境变量）

	vim /etc/profile #不同的服务器profile文件的位置会有变化

在配置文件中加入以下配置：

>JAVA_HOME=/java/jdk1.8.0_231 
>JRE_HOME=/java/jdk1.8.0_231/jre     
>CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
>PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
>export JAVA_HOME JRE_HOME CLASS_PATH PATH

#其中的文件位置请自行修改
修改完毕之后，记得使其生效

	source /etc/profile

# 测试

查询安装的java版本

	java -version

如果显示版本则说明jdk安装成功

![2](https://1716416169.github.io/安装java环境（linux环境）/2.png)

# 常用指令

	java -jar --server.port=xxx #启动的端口





