---
title: git的使用
date: 2019-12-19 20:50:12
tags: 
- git
categories: 
- 教程
- 笔记
---

# 前言
Git是一个开源的分布式版本控制系统，对于代码或文件的迭代管理有着巨大的帮助。

# git的工作流程

![image-20200221221507248](demo2.assets/image-20200221221507248.png)

# 设置

使用Git前，需要给使用者设置一个标识（就是给你自己取名）

		git config --global user.name "weijianfeng"

# 创建版本库
其实就是新建一个文件夹作为一个放文件的仓库
只不过需要再创建好文件夹后初始化

		git init


# 将远程的仓库复制到本地来（git hub）

		git clone 你仓库的地址

# 加入新的文件
再修改文件后需要进行重新添加操作（将文件添加到暂存区）

		git add -A

ps：这个是添加全部的修改后的文件（省事）

# 提交文件
再完成add操作后，需要进行提交操作（将暂存区的文件提交到仓库）

		git commit -m “本次提交的备注”

# 检擦文件是否被修改

		git diff

# 将本地文件推送到远程仓库
再进行推送前，需要先与远程仓库进行关联

		git remote add origin 你远程仓库的地址

然后再进行推送操作

		git push -u origin master
ps:中途会让你输入账号密码

# 查看历史变更记录

		git log
		git log --pretty=oneline //使记录只显示一行

# 回退版本

		git reset --hard HEAD^
		git reflog: 获取历史版本号
		git reset --hard 版本号
