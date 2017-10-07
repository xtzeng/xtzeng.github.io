---
title: linux 常用命令
date: 2017-04-25 20:12:52
tags: [linux]
---

1.linux 命令格式

```bash
 command [-options] [parameter1] ···
```

说明：
·command:命令名，相应功能的英文单词或单词的缩写[-option]:选项，可用来对命令进行控制，也可以省略，[]代表可选 parameter1...:传递给命令的参数：可以是零个或多个

例：

```bash
ls -a /home/xiaoti
```

2.查看帮助文档

 <1>--help
一般是linux命令自带的帮助信息
如：ls --help
 <2>man(有问题找男人，manual) 
man是linux提供的一个手册,包含了绝大部分的命令，函数使用说明
该手册分成很多章节(section)，使用man时可以指定不同的章节来浏览
例：man ls; man 2 printf

man中各个section意义如下：
1.Standard commands(标准命令)
2.System calls(系统调用,如open,write)
3.Library functions(库函数，如printf,fopen)
4.Special devices(设备文件的说明,/dev下各种设备)
5.File formats(文件格式，如passwd)
6.Games and toys(游戏和娱乐) 
7.Miscellaneous(杂项、惯例和协定等，例如Linux档案系统、网络协定、ASCII码、environ全局变量)
8.Administrative Commands(管理员命令，如ifconfig)

man是按照手册的章节号的顺序进行搜索的。 

man设置了如下的功能键

| 功能键      |    功能 |
| :-------- | --------:|
| 空格键  | 显示手册页的下一屏 |
| Enter键     |   一次滚动手册页的一行 |
| b      |    回滚一屏 |
| f      |    前滚一屏 |
| q      |    退出man命令 |
| h      |    列出所有功能键 |
| /word      |    搜索word字符串 |