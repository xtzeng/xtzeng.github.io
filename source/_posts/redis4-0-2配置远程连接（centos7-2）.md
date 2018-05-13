---
title: redis4.0.2配置远程连接（centos7.2）
date: 2018-05-14 00:52:01
tags: [redis]
---


最近开始学习redis，在服务器上安装了redis之后，远程连接一直连接不上，报错如下：

 redis.clients.jedis.exceptions.JedisConnectionException: java.net.ConnectException: Connection refused: connect

总结原因如下：
1、6379端口没有开放
2.修改redis.conf配置文件

这个文件需要修改两个地方

打开redis.conf文件
　　按crrl+F查询，

找到bind 127.0.0.1，把这行前面加个#注释掉
再查找protected-mode yes 把yes修改为no，然后：wq保存文件，
把服务关掉

redis远程连接命令:redis-cli -h 127.0.0.1 -p 6379

