---
title: mysql 'root'@'localhost'无法登录
date: 2017-10-22 11:43:05
tags: [mysql]
---

MySQL 'root'@'localhost'无法登录


		#mysql -u root -p 
提示”Access denied for user ‘root’@’localhost’ (using password: YES)”

远程可以登录，本地不能登录，原因是没有授权本地登录，使用命令

	select Host,User,Password from mysql.user;

![mysql-grant](http://oncykm32h.bkt.clouddn.com/mysql_grant.png)

使用命令：
	
	grant all privileges on dbName.* to 'root'@'localhost' identified by '123456' with grant option;

 	flush privileges ;


