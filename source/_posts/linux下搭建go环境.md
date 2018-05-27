---
title: linux下搭建go环境
date: 2018-05-27 01:01:37
tags: [linux]
---

安装go工具

在 http://golang.org/dl/下载最新的linux版本，并把它提取到/usr/local目录，在此目录下进行解压缩

	$ tar -xvf xxx.tar.gz 

然后将/usr/local/go/bin添加到PATH环境变量中，执行

    $ vim /etc/profile
	$ export PATH=$PATH:/usr/local/go/bin
    $ source /etc/profile


实际上go会默认假定它被安装到/usr/local/go目录下，但也可以将go安装到其他位置，此时必须设置GOROOT环境变量来指出它所安装的位置。

执行go version，看到go的安装版本即安装成功

第一个hello world 程序

GOPATH环境变量指定了你的工作空间位置

首先创建一个工作目录，并设置相应的GOPATH，工作目录可以放在任何地方，但不能和go的安装目录相同，在这我们使用$HOME/work

	$ mkdir $HOME/work 
	$ vim /etc/profile 
	$ export GOPATH=$HOME/work  

注意：go的代码必须放在工作空间内，也就是我们这里的work目录下，其中包含了三个子目录

	bin目录包含可执行命令
	
	pkg目录包含包对象
	
	src目录包含go的源文件，它们被组织成包（每个目录都对应一个包）

接下来将工作空间的bin子目录添加到PATH中：


	$ vim /etc/profile
	$ export PATH=$PATH:$GOPATH/bin
    $ source /etc/profile

包路径：
标准库中的包有给定的短路径比如"fmt"，对于你自己的包，也必须选择一个基本路径，来保证它不会与将来添加到标准库或其他标准库中的包相冲突。

使用packs作为基本路径，在你的工作空间里创建一个目录，我们将源码放在其中：

	mkdir $GOPATH/src/packs 

要编译运行简单的程序，首先要选择包路径，在这里我们使用packs/hello，并在你的工作空间内创建相应的包目录：

	$ mkdir $GOPATH/src/packs/hello  

接着在该目录中创建名为hello.go的文件，其内容如下

	package main  
  
	import "fmt"  
  
	func main() {  
    	fmt.Printf("Hello, world.\n")  
	} 

现在可以使用go工具构建并安装此程序了

	$ go install packs/hello 

注意，你可以在系统的任何地方运行此命令。go工具会根据GOPATH指定的工作空间，在packs/hello包内查找源码。
如果从包目录中运行go install，也可以省略包路径：

	$ cd $GOPATH/src/packs/hello  
	$ go install

此命令会构建hello命令，产生一个可执行的二进制文件。并存放在工作空间的bin目录下，在这里就是$GOPATH/bin目录下
因为已经将$GOPATH/bin添加到PATH中，只需要输入该二进制文件名执行即可

	$ hello  
	Hello, world. 


