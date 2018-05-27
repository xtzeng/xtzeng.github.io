---
title: eclipse debug启动老是跳转到断点，提示SilentExitException
date: 2018-05-15 11:21:28
tags: [eclipse]
---

最近在做一个spring boot的项目，在main方法debug启动的时候，老是自动跳转到断点，如下图所示

![silentExitException](http://oncykm32h.bkt.clouddn.com/20180228175121654.png)

出现这种状况是因为Eclipse默认开启挂起未捕获的异常(Suspend execution on uncaught exceptions)，只要关闭此项就可以了。

解决方法：在eclipse中选择Window->Preference->Java->Debug，将“Suspend execution on uncaught exceptions”的勾去掉即可。
