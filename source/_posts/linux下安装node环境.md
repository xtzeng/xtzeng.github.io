---
title: linux下安装node环境
date: 2017-10-07 13:46:43
tags: [linux]
---

首先去官网下载代码，这里一定要注意安装分两种，一种是Source Code源码，一种是编译后的文件。

![nodejs-download](http://oncykm32h.bkt.clouddn.com/nodejs-download.png)

（一） 编译好的文件

  简单说就是解压后，在bin文件夹中已经存在node以及npm，如果你进入到对应文件的中执行命令行一点问题都没有，不过不是全局的，所以将这个设置为全局就好了。

		cd node-v0.10.28-linux-x64/bin
        ls
        ./node -v

然后设置全局：

    ln -s /opt/java/node-v6.11.4-linux-x64/bin/node /usr/local/bin/node
    ln -s /opt/java/node-v6.11.4-linux-x64/bin/npm /usr/local/bin/npm

这里/home/kun/mysofltware/这个路径是你自己放的，你将node文件解压到哪里就是哪里。


（二）通过源码编译

这种方式你下载的文件是Source code，

		#  tar xvf node-v0.10.28.tar.gz 
		#  cd node-v0.10.28 
		#  ./configure 
		# make 
		# make install 
		# cp /usr/local/bin/node /usr/sbin/ 
 
查看当前安装的Node的版本
 
		# node -v 
		v6.11.4

（三）apt-get


还有一种就是shell提示的apt-get方式
 
    sudo apt-get install nodejs
	sudo apt-get install npm

这么装完你会发现,node命令好使，nodejs命令可以用
