---
title: git一些常用命令
date: 2017-04-12 21:10:44
tags:
---


1.怎么用git删除远程分支？
git v1.7.0之后，可以使用一下语法删除远程分支.
```bash
$ git push origin --delete <branchName>
```

删除tag可以使用命令：
```bash
$ git push origin --delete tag <tagName>
```

还可以使用推送一个空分支到远程分支的方式来删除远程分支：
```bash
git push origin :<branchName>
```

2.本地项目文件夹推送到git远程仓库一般步骤

```bash
git init
```

git add  (文件名)   
注意:使用git add命令添加需要上传的文件到缓存中,而不是上传过去
```bash
git add .
```

```bash
git commit -m "message"
```

```bash
git remote add origin https://github.com/xtzeng/xmq-spring-transation-parent.git
``` 

我们第一次push的时候,加上-u参数,Git就会把本地的master分支和远程的master分支进行关联起来,我们以后的push操作就不再需要加上-u参数了
```bash
git push -u origin master
```