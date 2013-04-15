---
layout: post
title: 在android平台上使用Git和SSH更新Github
categories: [Web]
tags: [Git, Github, SSH, Terminal IDE]
---

[上一篇](http://oooym.com/blog/Technology/2013/03/06/hello-jekyll.html)文章讲到，使用Jekyll+Github搭建笔记性博客，既然定义为笔记性，那么应该要求做到随处可记。在移动互联网日益繁盛的今天，这篇日志来探讨如何在Android移动平台上同步和发表文章。Github要求用到SSH和Git，那么这里推荐一款Android App [Terminal IDE](http://www.spartacusrex.com/terminalide.htm)，这是一个包含了`ssh`、`git`及一些linux平台基本命令的软件包，下载地址在[这里](http://code.google.com/p/terminal-ide/)。

下载安装好之后，我们就可以进入正题了。

1. 打开Terminal IDE，克隆Github上的项目到Android平台上。
		git clone https://github.com/username/blog.git
2. 切换到克隆的项目目录下，在相应位置新建Markdown格式笔记，同时注意遵循Jekyll规范。这里推荐一款Android上的文本编辑器[Jota Text Editor](https://play.google.com/store/apps/details?id=jp.sblo.pandora.jota)。
3. 拷贝PC平台家目录下的`.ssh`文件至Android的`~/.ssh`，当然也可以在Android上生成自己的rsa密钥文件再上传到Github。
4. 使用`git push`命令上传本地项目更新到Github，到这里我们就能在Android平台上上传文章啦。


>如果Android上本地版本和Github未进行同步更新导致不能`git push`成功，怎么办？

此时我们必须从远程分支下载最新版本到本地，有两种方式：	
	git fetch origin master(gh-pages)
	git merge origin/master(gh-pages)
	#或
	git pull origin master(jekyll)
	
			
##Thanks To:
[SSH and GIT on Android with Terminal IDE](http://tinyrobot.co.uk/blog/ssh-and-git-on-android-with-terminal-ide/)	
[Git fetch和git pull的区别](http://blog.csdn.net/hudashi/article/details/7664457)
		

