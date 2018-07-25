---
title: 'git add,git commit 填加错文件撤销'
date: 2018-06-06 11:51:37
tags: [git]
---

	1. git add 添加 多余文件 
这样的错误是由于， 有的时候 可能

git add . （空格+ 点） 表示当前目录所有文件，不小心就会提交其他文件

git add 如果添加了错误的文件的话

撤销操作

git status 先看一下add 中的文件 

git reset HEAD 如果后面什么都不跟的话 就是上一次add 里面的全部撤销了 

git reset HEAD XXX/XXX/XXX.java 就是对某个文件进行撤销了

	2. git commit 错误

如果不小心 弄错了 git add后 ， 又 git commit 了。
 
先使用 

git log 查看节点 

	commit xxxxxxxxxxxxxxxxxxxxxxxxxx 
	Merge: 
	Author: 
	Date:

然后 

	git reset commit_id

over

PS：还没有 push 也就是 repo upload 的时候


git reset commit_id （回退到上一个 提交的节点 代码还是原来你修改的） 

git reset –hard commit_id （回退到上一个commit节点， 代码也发生了改变，变成上一次的）


	3.如果要是 提交了以后，可以使用 git revert

还原已经提交的修改 

此次操作之前和之后的commit和history都会保留，并且把这次撤销作为一次最新的提交 

git revert HEAD 撤销前一次 commit 

git revert HEAD^ 撤销前前一次 commit
 
git revert commit-id (撤销指定的版本，撤销也会作为一次提交进行保存） 

git revert是提交一个新的版本，将需要revert的版本的内容再反向修改回去，版本会递增，不影响之前提交的内容。
