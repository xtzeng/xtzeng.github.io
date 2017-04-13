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