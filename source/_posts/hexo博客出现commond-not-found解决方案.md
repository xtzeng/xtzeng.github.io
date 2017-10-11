---
title: hexo博客出现commond not found解决方案
date: 2017-10-12 02:34:35
tags: [hexo]
---

		hexo -v
出现了conmand not found的提示

![hexo-command-not-found](http://oncykm32h.bkt.clouddn.com/hexo-command%20not%20found.png)


 按照字面上的翻译就是 找不到所使用的命令。我猜想可能是好久没有使用的原因了，于是按照以前的安装教程重新安装了一次安装教程，安装完毕之后，发现还是存在上面的问题，于是去请教大神，先查看各种工具是否都安装好了，在命令行中输入node -v 然后再检查npm -v。

![npm-v](http://oncykm32h.bkt.clouddn.com/npm%20-v.png)

    结果发现这里也没有问题。所以就可能是环境变量的问题，这里我突然想起可能是上次配置JAVA环境变量的时候，可能把这个环境变量搞错了，所以这里先去找到这个路径，C:\Users\xiaoti\node_modules\hexo\bin ，然后把它添加到环境变量PATH路径的后面。


![path](http://oncykm32h.bkt.clouddn.com/path.png)

配置下环境变量，hexo就恢复正常了