---
title: linux下安装配置nexus
date: 2017-10-08 02:43:55
tags: [linux]
---

为什么要搭建maven私服？

在开发过程中，有时候会使用到公司内部的一些开发包，显然把这些包放在外部是不合适的。另外，由于项目一直在开发中，这些内部的依赖可能也在不断的更新。可以通过搭建公司内部的Maven服务器，将第三方和内部的依赖统一管理，同时也可以节省网络带宽，当然前提是项目所需要的构件在私服中已经存在。

Nexus下载及安装配置

我们可以在nexus的官网上找到它的相关介绍，下载地址是：http://www.sonatype.org/nexus/go

 下载

 	# wget https://sonatype-download.global.ssl.fastly.net/nexus/oss/nexus-2.11.2-03-bundle.tar.gz

 解压

	# cd /usr/local
 	# mkdir nexus
 	# tar -zxvf /opt/java/nexus-2.14.5-02-bundle.tar.gz -C /usr/local/nexus
 	# cd nexus
 	# ls (显示如下两个文件夹)
 	nexus-2.11.2-03   sonatype-work

修改配置文件

 	# cd nexus-2.11.2-03/conf
 	# vi nexus.properties
 	#Jetty section
 	application-port=8081      ##修改Jetty端口号
 	# nexus section
 	nexus-work=${bundleBasedir}/../sonatype-work/nexus　

保存以上修改

配置用户

	# vi /usr/local/nexus/nexus-2.11.2-03/bin/nexus

	#RUN_AS_USER=

	RUN_AS_USER=root

保存以上修改

若有设置防火墙，需前往修改防火墙配置并重启防火墙，此处略过......

启动nexus

	# /usr/local/nexus/nexus-2.11.2-03/bin/nexus start
	
	****************************************

	WARNING - NOT RECOMMENDED TO RUN AS ROOT
	
	****************************************

	Starting Nexus OSS...

	Started Nexus OSS.

在浏览器打开:http://ip:8081/nexus,登录：用户名admin  默认密码：admin123

在项目中修改maven仓库地址

这样就配置完成了。在构建maven项目时，如果在私服中存在需要的构件，则会直接从私服中下载；如果私服中没有所需构件，则会先从网络上下载到私服，之后才会下载到本地。
