---
title: linux git clone ssl connect error
date: 2018-05-28 02:03:17
tags: [linux,git]
---


linux下 git clone 出现
	
	fatal: unable to access 'https://github.com/angular/bower-angular.git/': SSL connect error 

升级 nss curl libcurl 就好了

   分别执行 

	yum update nss
    yum update curl
    yum update libcurl
