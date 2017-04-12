---
title: 开始使用hexo写自己的blog
date: 2017-04-12 18:37:58
tags:
---


about hexo about markdown
====================

 一直想搭建一个属于自己的博客，以前都是在csdn或博客园上面写，最近一直在搭建github的hexo博客，折腾了几天时间，终于可以小试牛刀写点属于自己的东西，日后某一天回来看的时候，也许觉得那时候的自己是个煞笔，但能有所成长，也就足够了。以下是关于这几天在github搭建hexo的一些心得。

关于在不同的电脑（系统）上使用hexo
---------------------

将自己的blog文件夹使用git来管理，需要注意一下几点：
1.如果主题是通过git管理的，需要将主题文件夹下的.git文件夹删除，才能同步blog文件夹。（如果.git文件夹是隐藏的，需要显示隐藏文件才能删除，linux下用命令rm -rf命令删除）
2.按照blog目录下自带的.gitignore文件，node_modules文件夹是不会同步的，所以同步之后需要自己再次npm install,但是要注意一点，不要再进行hexo init了，否则 _config.yml就全都白弄了

必须拷贝的文件：
_config.yml,theme文件夹里面的主题，以及source里面自己写的blog文件,这些肯定是要拷贝的.
除此之外还有三个文件需要保留，就是scaffolds文件夹(文章的模板)、packeage.json(说明使用哪些包) 还有.gitignore(限定在提交的时候哪些文件可以忽略)。其实这三个文件不用我们修改的，所以
即使丢失了也没有关系，我们可以另外新建一个临时文件夹，然后在里面执行hexo init,就可以生成这三个文件，我们只需要将它们拷贝过来使用即可。
总结：_config.yml、theme/、source/、scaffolds/、package.json、.gitignore是需要备份的。

然后我们再考虑哪些文件是不需要拷贝、或者说可以删除的
首先是.git文件夹，无论是在站点根目录下，还是主题目录下的.git文件，都可以删掉。然后是文件夹node_modules(在用npm install 会重新生成)、public文件夹(这个在使用命令hexo g后会重新生成)，deploy_git文件夹(在使用hexo d后也会重新生成),还有db.json文件.其实这些文件也就是.gitignore文件里面记载的内容.
总结：.git/、node_modules/、public/、deploy_git/、db.json文件可以删除