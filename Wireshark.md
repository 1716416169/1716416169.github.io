---
title: Wireshark教程
date: 2019-12-19 20:50:12
tags: 
- Wireshark
categories: 
- 教程
- Wireshark

---

# 前言

无

## Wireshark界面

![1](C:%5CUsers%5Ccoder%5CDesktop%5Chexo%5Cwireshark%5C1.png)
由上图：
 WireShark 主要分为这几个界面

1. Display Filter(显示过滤器)，  用于过滤
2. Packet List Pane(封包列表)， 显示捕获到的封包， 有源地址和目标地址，端口号。 颜色>不同，代表
3. Packet Details Pane(封包详细信息), 显示封包中的字段
4. Dissector Pane(16进制数据)
5. Miscellanous(地址栏，杂项)

## 显示过滤器
用来在捕获的记录中找到所需要的记录

## 封包列表
封包列表的面板中显示，编号，时间戳，源地址，目标地址，协议，长度，以及封包信息。 你可以看到不同的协议用了不同的颜色显示。

## 封包详细信息
Frame:   物理层的数据帧概况

Ethernet II: 数据链路层以太网帧头部信息

Internet Protocol Version 4: 互联网层IP包头部信息

Transmission Control Protocol:  传输层T的数据段头部信息，此处是TCP

Hypertext Transfer Protocol:  应用层的信息，此处是HTTP协议

