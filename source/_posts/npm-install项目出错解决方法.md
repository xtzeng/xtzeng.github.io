---
title: npm install项目出错解决方法
date: 2017-10-12 02:54:36
tags: [nodejs]
---

	108629 error Windows_NT 10.0.10586
	108630 error argv "D:\\Program Files\\nodejs\\node.exe" "D:\\Program Files\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "install"
	108631 error node v5.6.0
	108632 error npm v3.6.0
	108633 error code ELIFECYCLE
	108634 error phantomjs@1.9.19 install: node install.js
	108634 error Exit status 1
	108635 error Failed at the phantomjs@1.9.19 install script 'node install.js'.
	108635 error Make sure you have the latest version of node.js and npm installed.
	108635 error If you do, this is most likely a problem with the phantomjs package,
	108635 error not with npm itself.
	108635 error Tell the author that this fails on your system:
	108635 error node install.js
	108635 error You can get information on how to open an issue for this project with:
	108635 error npm bugs phantomjs
	108635 error Or if that isn't available, you can get their info via:
	108635 error npm owner ls phantomjs
	108635 error There is likely additional logging output above.
	108636 verbose exit [ 1, true ]

解决方法：

删除npmrc文件，使用镜像

	npm iconfig set registry http://registry.cnpmjs.org
	npm info underscore
