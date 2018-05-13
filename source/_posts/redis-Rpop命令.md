---
title: redis Rpop命令
date: 2018-05-14 01:02:36
tags: [redis]
---


Redis Rpop 命令

Redis Rpop 命令用于移除并返回列表的最后一个元素。


语法
redis Rpop 命令基本语法如下：

	redis 127.0.0.1:6379> RPOP KEY_NAME 

返回值
列表的最后一个元素。 当列表不存在时，返回 nil 。

实例

	redis> RPUSH mylist "one"
	(integer) 1
	redis> RPUSH mylist "two"
	(integer) 2
	redis> RPUSH mylist "three"
	(integer) 3
	redis> RPOP mylist
	"three"
	redis> LRANGE mylist 0 -1
	1) "one"
	2) "two"
	redis> 