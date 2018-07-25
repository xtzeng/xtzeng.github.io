---
title: windows下安装rabbitMQ
date: 2018-06-12 16:36:48
tags: [windows,rabbitMQ]
---

1.Windows下安装RabbitMQ需要以下几个步骤

 (1)：下载erlang，原因在于RabbitMQ服务端代码是使用并发式语言erlang编写的，下载地址：http://www.erlang.org/downloads，双击.exe文件进行安装就好，安装完成之后创建一个名为ERLANG_HOME的环境变量，其值指向erlang的安装目录，同时将%ERLANG_HOME%\bin加入到Path中，最后打开命令行，输入erl，如果出现erlang的版本信息就表示erlang语言环境安装成功；


(2)：下载RabbitMQ，下载地址：http://www.rabbitmq.com/，同样双击.exe进行安装就好(这里需要注意一点，默认的安装目录是C:/Program Files/....，这个目录中是存在空格符的，我们需要改变安装目录，貌似RabbitMQ安装目录中是不允许有空格的，我之前踩过这个大坑)；

 (3)：安装RabbitMQ-Plugins，这个相当于是一个管理界面，方便我们在浏览器界面查看RabbitMQ各个消息队列以及exchange的工作情况，安装方法是：打开命令行cd进入rabbitmq的sbin目录(我的目录是：E:\software\rabbitmq\rabbitmq_server-3.6.5\sbin)，输入：rabbitmq-plugins enable rabbitmq_management命令，稍等会会发现出现plugins安装成功的提示，默认是安装6个插件,这样，就安装好插件了，是不是能使用了呢？别急，需要重启服务才行，使用命令：
	
	net stop RabbitMQ && net start RabbitMQ

这时候的，也许会出现这种结果：

“发生错误：发生系统错误 5。  拒绝访问。”

这是什么鬼？查了下，原来，5代表的是：不是系统管理员权限。

问题解决方案：使用管理员打开cmd再执行此命令：



 (4)：插件安装完之后，在浏览器输入http://localhost:15672进行验证，你会看到下面界面，输入用户名：guest，密码：guest你就可以进入管理界面，当然用户名密码你都可以变的；

