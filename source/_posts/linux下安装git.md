---
title: linux下安装git
date: 2018-05-28 01:41:13
tags: [linux]
---

Git是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。而国外的GitHub和国内的Coding都是项目的托管平台。但是在使用Git工具的时候，第一步要学会如何安装git，本教程就手把手教大家如何手动编译安装git。

1、介绍

　　使用Coding管理项目，上面要求使用的git版本为1.8.0以上，而很多yum源上自动安装的git版本为1.7，所以需要掌握手动编译安装git方法。

2、安装git依赖包


     yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel gcc perl-ExtUtils-MakeMaker
3、删除已有的git

	yum remove git

4、下载git源码

　　切换到你的包文件存放目录下
　　			

    	cd /usr/src

下载git安装包


	wget https://www.kernel.org/pub/software/scm/git/git-2.8.3.tar.gz

　　解压git安装包				
		
	tar -zxvf git-2.8.3.tar.gz　　
	cd git-2.8.3

　　配置git安装路径　
		
	./configure prefix=/usr/local/git/

　　编译并且安装　　　　

	make && make install

　　查看git版本号　　	
		
	cd /usr/local/git/bin

	git --version

　　git已经安装完毕

5、将git指令添加到bash中
　
	
	vi /etc/profile

　　在最后一行加入
		
	export PATH=$PATH:/usr/local/git/bin

　　让该配置文件立即生效
		
	source /etc/profile
