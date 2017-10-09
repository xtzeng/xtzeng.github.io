---
title: linux下修改防火墙配置重启命令
date: 2017-10-09 18:12:08
tags: [linux]
---

1.  在/etc/sysconfig/iptables里添加

		# vi /etc/sysconfig/iptables
添加一条配置规则，如要想开放8080的端口，如下所示：

		-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 –j ACCEPT

2. 重启iptables

		# /etc/init.d/iptables restart

3. 看下状态

		# /etc/init.d/iptables status

4.关闭防火墙

（1） 重启后永久性生效：

	开启：chkconfig iptables on 
	关闭：chkconfig iptables off

（2） 即时生效，重启后失效（即重启后防火墙自动开启）：

	开启：service iptables start
	关闭：service iptables stop
