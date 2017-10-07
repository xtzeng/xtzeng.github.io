---
title: linux下安装pm2
date: 2017-10-07 14:15:55
tags: [linux]
---

如果可以联网

     直接执行：npm install -g pm2

登录部署服务器

执行 npm config get prefix 看一下这台服务器的npm默认安装目录， 例如目录为 ：

	/opt/java/node-v6.11.4-linux-x64

到这一步，你已经可以使用 /opt/java/node-v6.11.4-linux-x64/lib/node_modules/pm2/bin/pm2 执行pm2的命令了， 下面就是把这个命令加到系统环境中

   	ln -s /opt/java/node-v6.11.4-linux-x64/lib/node_modules/pm2/bin/pm2 /usr/local/bin/pm2

下面就是把这个命令加到系统环境中

这样，就可以直接使用pm2命令来各种操作了

