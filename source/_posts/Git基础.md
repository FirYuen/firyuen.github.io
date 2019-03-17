---
title: Git基础
---
按照课程安排，写几个Git基础命令。


## git init

### 用 git init 在目录中创建新的 Git 仓库。 你可以在任何时候、任何目录中这么做，完全是本地化的。在目录中执行 git init，就可以创建一个 Git 仓库了。

``` bash
$ mkdir gitlearn
$ cd gitlearn/
$ git init
Initialized empty Git repository in /Users/yuanpengfei/gitlearn/.git/
```

## git add

### git add 命令可将该文件添加到缓存，如我们添加以下两个文件：
```bash
$ touch README
$ touch index.html
$ ls
README        index.php
$ git status -s
?? README
?? index.php
$ git add README index.html
$ git status -s
A README
A index.php
```
## git commit -v

### 显示有哪些更改

## 关于更多Git命令
能记得尽量记，不记得的话用的时候查
[菜鸟教程](http://www.runoob.com/git/git-tutorial.html)
