---
title: 使用hexo，如果更换了电脑如何更新博客
date: 2017-10-05 09:46:26
tags: [hexo]
---

一、关于搭建的流程

1.创建仓库:xtzeng.github.io;

2.创建两个分支：master和hexo;

3.设置hexo为默认分支（因为我们只需要手动管理这个分支上的hexo网站文件）;

4.git clone https://github.com/xtzeng/xtzeng.github.io.git拷贝仓库（hexo分支-默认）;

5.在本地xtzeng.github.io文件夹下通过git bash依次执行npm install hexo、hexo init、npm install和npm install hexo-deployer-git(此时当前分支应显示为hexo);

6.修改_config.yml中的deploy参数，分支应为master;

7.依次执行git add .、git commit -m "..."、git push origin hexo提交网站相关的文件；

8.执行hexo g -d 生成网站并部署到github上；

这样一来，在github上的xtzeng.github.io仓库就有两个分支，一个hexo分支用来存放网站的文件，一个master分支用来存放生成的静态文件。

二、关于日常的流程改动

在本地对博客进行修改（添加新博客、修改样式等等）后，通过下面的流程进行管理。

1.依次执行git add .、git commit -m "..."、git push origin hexo指令将改动推送到github(此时当前分支应为hexo);

2.然后才执行hexo g -d 发布到master分支上。

虽然两个过程顺序调转一般不会有问题，不过逻辑上这样的顺序是绝对没有问题的（例如突然死机要重装了，悲催...的情况，调转顺序就有问题了）。

三、本地资料丢失后的流程

当重装电脑之后，或者想在其他电脑上修改博客，可以使用以下步骤：

1.使用git clone https://github.com/xtzeng/xtzeng.github.io.git 拷贝仓库（默认分支为hexo）;

2.在本地新拷贝的xtzeng.github.io文件夹下通过git bash依次执行以下指令：npm install hexo、npm install、npm install hexo-deployer-git(记得，不需要hexo init 这条指令)

