---
title: hexo添加搜索服务
date: 2017-10-15 02:11:26
tags: [hexo]
---

在hexo->NexT主题下添加搜索服务

NexT 支持集成 Swiftype、 Local Search 和 Algolia。

1.安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：

	$ npm install hexo-generator-searchdb --save

2.编辑 站点配置文件，新增以下内容到任意位置：

	search:
	  path: search.xml
	  field: post
	  format: html
	  limit: 10000

3.编辑 主题配置文件，启用本地搜索功能：

	# Local search
	local_search:
	  enable: true

另外介绍其他两个插件

一、给博客添加feed

1.安装hexo-generator-feed
	$ npm install hexo-generator-feed --save

2.配置到站点配置文件_config.yml

	
	# Extensions
	## Plugins: http://hexo.io/plugins/
	#RSS订阅
	plugin:
	- hexo-generator-feed
	#Feed Atom
	feed:
	type: atom
	path: atom.xml
	limit: 20

3.最后，在你next主题下的_config.yml下，添加RSS订阅链接即可：

	rss: /atom.xml

二、给博客生成一个站点地图

1.安装hexo-generator-seo-friendly-sitemap

	$ npm install hexo-generator-seo-friendly-sitemap --save

2.在站点配置文件_config.yml 中添加

	sitemap:
    path: sitemap.xml

