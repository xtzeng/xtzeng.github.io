---
title: git push命令
date: 2018-05-28 10:56:27
tags: [git]
---

git push命令用于将本地分支的更新，推送到远程主机。它的格式与git pull命令相似。

	$ git push <远程主机名> <本地分支名>:<远程分支名>

示例

	$ git push origin master

上面命令表示，将本地的master分支推送到origin主机的master分支。如果master不存在，则会被新建。

如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。

	$ git push origin :master
	# 等同于
	$ git push origin --delete master

上面命令表示删除origin主机的master分支。如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。

	$ git push origin

上面命令表示，将当前分支推送到origin主机的对应分支。如果当前分支只有一个追踪分支，那么主机名都可以省略。

	$ git push

如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用git push。

	$ git push -u origin master	

上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

	$ git push --all origin

上面命令表示，将所有本地分支都推送到origin主机。
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做git pull合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用–force选项。

	$ git push --force origin

上面命令使用-–force选项，结果导致在远程主机产生一个”非直进式”的合并(non-fast-forward merge)。除非你很确定要这样做，否则应该尽量避免使用–-force选项。

最后，git push不会推送标签(tag)，除非使用–tags选项。

	$ git push origin --tags


