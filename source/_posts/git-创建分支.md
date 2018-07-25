---
title: git 创建分支
date: 2018-06-05 19:24:07
tags: [git]
---

	$ git checkout -b iss53
	Switched to a new branch 'iss53'

这相当于执行下面这两条命令：

	$ git branch iss53
	$ git checkout iss53


1.git branch

不带参数：列出本地已经存在的分支，并且在当前分支的前面用"*"标记

2.git branch -r

查看远程版本库分支列表

3.git branch -a

查看所有分支列表，包括本地和远程

4.git branch dev

创建名为dev的分支，创建分支时需要是最新的环境，创建分支但依然停留在当前分支

5.git branch -d dev

删除dev分支，如果在分支中有一些未merge的提交，那么会删除分支失败，此时可以使用 git branch -D dev：强制删除dev分支，

6.git branch -vv 

可以查看本地分支对应的远程分支

7. git branch -m oldName newName

给分支重命名

Git checkout

1. 操作文件  2. 操作分支

 		git checkout filename 放弃单个文件的修改

 		git checkout . 放弃当前目录下的修改

git checkout master 将分支切换到master

git checkout -b master 如果分支存在则只切换分支，若不存在则创建并切换到master分支，repo start是对git checkout -b这个命令的封装，将所有仓库的分支都切换到master，master是分支名，

