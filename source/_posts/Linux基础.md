---
title: Linux基础
date: 2018-05-13 15:55:40
tags:
---
写几个Linux基础命令。


## ls

### 查看当前目录下的文件

``` bash
$ ls
Applications    Documents	Library		Music		Public
Desktop		Downloads	Movies		Pictures
```
### 以列表方式查看当前目录下文件
``` bash
$ ls -l
total 0
drwx------@  4 yuanpengfei  staff   128  5 12 12:58 Applications
drwx------+  9 yuanpengfei  staff   288  5 13 17:12 Desktop
drwx------+  8 yuanpengfei  staff   256  5 13 19:57 Documents
drwx------+ 10 yuanpengfei  staff   320  5 13 17:49 Downloads
drwx------@ 61 yuanpengfei  staff  1952  5 13 17:30 Library
drwx------+  3 yuanpengfei  staff    96  5 12 00:25 Movies
drwx------+  4 yuanpengfei  staff   128  5 12 23:05 Music
drwx------+  3 yuanpengfei  staff    96  5 12 00:25 Pictures
drwxr-xr-x+  4 yuanpengfei  staff   128  5 12 00:25 Public
``` 
### 显示当前目录下所有文件，包括隐藏文件
``` bash
$ ls -a
.			.config			Desktop
..			.gitconfig		Documents
.CFUserTextEncoding	.node_repl_history	Downloads
.DS_Store		.npm			Library
.ShadowsocksX-NG	.oracle_jre_usage	Movies
.Trash			.ssh			Music
.bash_history		.swt			Pictures
.bash_sessions		.vscode			Public
.bashrc			Applications
``` 

## cat

### 打印文件内容到终端上
```bash
$ cat .bashrc
alias ll="ls -l"
cd ~/Desktop/
```
## mv

### 将文件重命名或者移动到指定目录
```bash
$ ls
1.txt
$ mv 1.txt 2.txt
$ ls
2.txt
```

## touch

### 创建一个空白文件
```bash
$ ls
1.txt
$ touch 2.txt
$ ls
1.txt 2.txt
```

## explainshell.com
输入不认识的命令和后面的参数，explainshell会分辨解析命令的功能是什么，后面跟着的参数是什么，都是英文的，墙内的可以参考这个网站[Linux命令大全](http://man.linuxde.net)