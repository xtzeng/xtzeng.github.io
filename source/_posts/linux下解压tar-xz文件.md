---
title: linux下解压tar.xz文件
date: 2017-10-07 13:39:09
tags: [linux]
---

这个压缩包也是打包后再压缩，外面是xz压缩方式，里层是tar打包方式。

使用如下命令：

```js

	$xz -d ***.tar.xz

	$tar -xvf  ***.tar

```


   补充：目前也可以直接使用 tar xvJf  ***.tar.xz来解压

