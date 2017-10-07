---
title: linux下安装Subversion+Apache
date: 2017-10-06 23:30:27
tags: [linux]
---

root用户操作

建议安装前更新操作系统

```js

	# yum update

```

更新完成后重启

```js

	#reboot

```


安装apache

```js

	# yum install httpd httpd-devel
	# service httpd start
	# chkconfig httpd on    //配置httpd开机启动

```

```js

	#vi /etc/httpd/conf/httpd.conf

```

找到ServerName并修改成【ServerName localhost:80】

防火墙中打开80端口：

```js

	# vi /etc/sysconfig/iptables
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
	# service iptables restart

```

http://192.168.1.119/

![apage2-test-page](http://oncykm32h.bkt.clouddn.com/apache2-test-page.png)

安装SVN服务

```js

	# yum install mod_dav_svn subversion

```

必须安装mod_dav_svn模块

安装完svn后要重启apache

```js

	# service httpd restart

```

查看测试是否安装svn模块

```js

	# ls /etc/httpd/modules/ | grep svn
	  mod_authz_svn.so
	  mod_dav_svn.so
	# svn --version

```

在根目录下创建svn库主目录（多库模式，一份配置文件管理多个库）

```js

	# mkdir /svn/
	# cd/etc/httpd/conf.d
	# ls  

```

此时可以看到一个subversion.conf配置文件（是在安装mod_dav_svn模块时生成的）

```js

	# vi subversion.conf

```

添加以下内容

```js

	#Include /svn/httpd.conf
	<Location /svn/>
	DAV svn
	SVNListParentPath on
	SVNParentPath /svn
	AuthType Basic
	AuthName "Subversion repositories"
	AuthUserFile /svn/passwd.http
	AuthzSVNAccessFile /svn/authz
	Require valid-user
	</Location>
	RedirectMatch ^(/svn)$ $1/

```

创建/svn/passwd.http和/svn/authz

```js

	# touch /svn/passwd.http
	# touch /svn/authz

```

重启apache

```js

	# service httpd restart

```

重启成功说明我们添加的配置是没有问题的












