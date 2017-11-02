---
title: linux下配置网络静态ip
date: 2017-11-02 17:44:08
tags: [linux]
---

linux下配置网络静态ip

	vi /etc/sysconfig/network-scripts/ifcfg-eth0
    
	service network restart 或/etc/init.d/network restart


	
	DEVICE=eth0（设备名称）
	HWADDR=00：0c:29：d3:bb:e5 (mac地址)
	TYPE=Ethernet （网络类型）
    ONBOOT=yes (开机启动)
	BOOTTPROTO=static （静态ip）
	DNS1：192.168.1.1 (dns)
    IPADDR=192.168.1.45 （ip地址）
    NETMASK=255.255.255.0 (子网掩码)
    GATEWAY=192.168.1.1 （网关）


如果ping的是广域网而不是局域网，还要确保网关和DNS正确，
用命令route add default gw 192.168.1.1