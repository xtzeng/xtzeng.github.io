---
title: hexo添加tags
date: 2017-10-06 17:00:08
tags: [hexo]
---

## 步骤一

新建一个页面，命名为 tags 。命令如下：

```js

	$ hexo new page "tags"

```

## 步骤二

这时会在在sources/tags里面有个index.md的文件，打开这个文件编辑
将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：

```js

	title: Tagcloud
	date: 2014-12-22 12:39:04
	type: "tags"
	comments: false
	---

```

注意：如果有启用多说或者Disqus评论，默认页面也会带有评论。需要关闭的话，需要添加字段comments并将该值设置为false（如上）

## 步骤三

在菜单中添加链接。编辑 主题(这里以next为例)配置文件 ，添加 tags 到 menu 中，如下:

```js

	menu:
      home: /
      archives: /archives
      tags: /tags     //确保标签页已打开
	  #schedule: /schedule     
  	  #commonweal: /404.html

```

注意：所有冒号后面都有个空格

hexo一篇文章添加多个tags用法为：tags:[linux,c,c++]
