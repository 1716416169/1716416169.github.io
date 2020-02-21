---
title: servet+jsp+maven的使用
date: 2019-11-25 20:56:23
tags:
- jsp
- servlet
- maven
catepories:
- 教程
---
# 前言
servlet和jsp技术是java进行web开发所必学的技术，但你可能会说：servlet就算了，jsp这种完成被淘汰的技术为什么还要学习？问的好，技术都是循序渐进的，虽然他可能已经不被大众所待见，但他的编程思想以及建立在他之上的框架的设计思路不都是我们应该进行学习的原因吗。当然，我不否认他们的过时，所以本文将只对上述技术进行“浅”教程和初步的搭建运行。如有兴趣可自行深入学习。

# 什么是servlet？
 Servlet 是运行在 Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。
使用 Servlet，您可以收集来自网页表单的用户输入，呈现来自数据库或者其他源的记录，还可以动态创建网页。
通俗点说，就是一个运行在服务器上的java程序，servlet一般处理客户端发来的请求，然后进行一系列处理，并且可以向客服端发送html标签（字面意思，用输出语句发送），但因为要发送的页面标签过多，太冗余，被人们淘汰了一段时间。

# 什么是jsp？
JSP 与 PHP、ASP、ASP.NET 等语言类似，运行在服务端的语言。JSP 技术是以 Java 语言作为脚本语言的，JSP 网页为整个服务器端的 Java 库单元提供了一个接口来服务于HTTP的应用程序。
通俗点说，就是在一个html页面里嵌入java代码，一般是对数据的逻辑处理或者是连接数据库的操作，然后这些jsp页面在运行时会被编译器转换成servlet代码（就是java代码），编译成二进制文件后运行。因为比起servlet的java代码里嵌入html标签，jsp的html标签里嵌入java代码要好的多（从感官上和可读性上来说），所以曾在一段时间里取代了servlet。

# servlet和jsp有什么关系？
在编程开发的早些年代，大都使用jsp，因为web开发无非就是画面+数据的结合，而jsp都能完成这些需求，并且比起servlet可读性要高的多，但是随着软件需求的增加和功能的复杂化，html里嵌入的java代码越来越多，可读性开始下降，所以最后演变成jsp负责开发页面，而servlet负责开发数据处理逻辑，而在之后的很长一段时间，开发流程都是前端写好静态页面，然后交给后台去扣数据，嵌入java代码，但是这很明显是高耦合的，开发效率低下，所以有了现在的前后端分离，但这就不是这篇文章讨论的问题了。

# 快速搭建一个jsp+servlet项目（idea工具）

## maven的使用
此项目的依赖管理采用maven管理工具，而maven的具体应用方法请自行百度，这里就不过多赘述（如果你用gradle也行）

## 创建

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/1.png)

选中maven一行，next

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/2.png)

输入你的组和组织名称（随意）

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/3.png)

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/3.5.png)

继续，如果你电脑里安装过maven，或者你想用本地库，那么就选你自己的本地库

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/4.png)

完成

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/5.png)

记得点击自动导入依赖（你不选也没事，就是要自己下载）

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/6.png)

配置启动的tomcat

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/7.png)

选中你使用的tomcat（这里博主电脑里有下好的tomcat，所以直接选择本地就可以了），其中有例如端口 运行浏览器等配置，请根据自己的情况配置

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/8.png)

然后将你的项目部署到tomcat上，这里不选artifact也行（选了就是以文件夹的形式运行，不选就是以war包的形式运行）

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/9.png)

然后就是运行了

![示例图片](https://1716416169.github.io/servet+jsp+maven的使用/10.png)

ok,大功告成，一个servlet+jsp的项目已经搭建了起来
# 未完待续
