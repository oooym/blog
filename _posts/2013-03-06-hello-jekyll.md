---
layout: post
title: Hello Jekyll!
categories: [Web]
tags: [Jekyll, Github, Markdown]
---

国际惯例，每到一个新的平台上第一个例程当是`Hello World`。这里也不例外，写下这篇`Hello Jekyll`记录本博客搭建过程，姑且认为是一篇教程吧。当然，独立博客程序见得最多的当属Wordpress（WP）了，我并属于不是从WP平台转到Jekyll的，我也并不反感WP，那么为何放着WP这样的上乘之作不用，跑过来折腾Jeklly呢？我总结了几点：

- 我希望一套博客系统只有单一功能，不希望被诸如模板、主题、插件等干扰
- 我不喜欢数据库，讨厌心惊胆颤担心数据库丢失（我懒得备份）
- 我经常会做一些文本格式的笔记，而[Markdown](http://daringfireball.net/projects/markdown/)是绝佳选择
- ...	

如果这也正好契合于你，那么，你可以继续往下看..

一、Github与Jeklly
======

如果你是程序员就一定听说过[Github](https://github.com/)，如果没听说过也没关系。简单的来说，它是一个代码云存储的平台，是一个具有版本管理功能的代码仓库，存放着项目的源代码。但是对于一个新手或者完全通程序的人来说，看到一大堆源码，无非跟看到一页页天书一样。他希望有一个简单易懂的README来告诉他每一步应该怎么做。因此，Github设计了Github Pages功能，允许用户自定义项目首页来替代使人头痛的源码列表。简单的来说，Github Pages就是托管于Github服务器上的静态网页。然而Github Pages有两种生成方式：

+ 利用Github提供的模板自动生成网页
+ 用户上传自己编写的静态网页

我们利用方式(2)，上传自己的网页，当然这里说的上传并不是单纯的上传，而是会经过Jekyll的处理。[Jekyll](http://jekyllrb.com/)是一个静态站点生成器，根据网页源码生成静态文件。而Github Pages的后台引擎就是Jekyll。Jekyll有自己的一套语法规范，具体参考[官方文档](https://github.com/mojombo/jekyll/wiki)。写到这里，思路就很明显了，现在本地编写符合Jeklly规范的网站源码，然后上传到Github，由Github生成并托管整个网站。看到这里有人会有疑问了，以为又要学习Jekyll的语法，然后自己写一套博客系统的静态网页。其实大可不必如此，类似的博客，[这里](https://github.com/mojombo/jekyll/wiki/Sites)已经有一大把大把了。所以我们要做的只剩写文章了，格式可以是HTML或Markdown。后面再做介绍。

二、Windows平台搭建本地Jekyll环境
======

1. 	下载安装[Github for Windows](http://windows.github.com/)。
2. 	下载安装[RubyInstaller](http://rubyinstaller.org/downloads/)，然后在命令行终端下输入`gem update --system`来升级gem。
3. 	下载安装[DevKit](http://rubyinstaller.org/add-ons/devkit/)，它是Windows下编译和使用本地C/C++扩展包的工具。安装方法如下：

		cd C:\DevKit
		ruby dk.rb init
		ruby dk.rb install

4. 	使用RubyGems的方式安装Jekyll：`gem install jekyll`，并使用`jekyll --version`或`jekyll -v`来检查是否安装成功。
5. 	一般而言还要安装Rdiscount这个用来解析Markdown标记语言的包：`gem install rdiscount`。

至此，Jekyll的本地环境就配置完成了。我们可以Clone Github上托管的[Jekyll项目](https://github.com/mojombo/jekyll/wiki/Sites)，当然也可以使用[Jekyll-bootstrap](https://github.com/plusjade/jekyll-bootstrap)。然后，打开命令行终端，进入到Clone的项目目录下，运行`jekyll --server --auto`，然后打开浏览器输入[http://127.0.0.1:4000]()进行访问。新手便可在这些项目里边寻找合适的，在本地修改、调试变成自己的网站。

三、推送本地项目到Github
======

Jekyll生成的网站仅仅能本地访问显然不是我们想要的，我们要把它推送到互联网上。先注册Github帐号，当然这是必须的，假定用户名为username(请将username换成你的用户名)。并且需要验证邮箱，否则可能无法正常使用Github Pages。然后创建个人仓库，这里我分为两种情况：

1. 	建立仓库“username.github.com”，注意此域名的第一部分和用户名要完全相同，这样的仓库可以通过[http://username.github.com]()根目录的方式来访问。上传步骤如下：

		#在命令行下进入要推送的项目目录下
		git init
		git add .
		git config --global user.email "你的email"
		git config --global user.name "你的名字"
		git commit -m "信息"
		git remote add origin https://github.com/username/username.github.com.git
		git push -u origin master

2. 	建立仓库“demo”，“demo”为任一合法仓库名称。这样的仓库通过[http://username.github.com/demo]()二级目录的方式来访问。上传步骤如下：

		git init
		git checkout --orphan gh-pages
		git add .
		git config --global user.email "你的email"
		git config --global user.name "你的名字"
		git commit -m "信息"
		git remote add origin https://github.com/username/username.github.com.git
		git push -u origin gh-pages

两种情况的区别在于方式(1)上传的master分支，方式(2)上传到gh-pages分支。更多Github知识请参见[这里](http://rogerdudler.github.com/git-guide/index.zh.html)。至此，我们已经可以通过Github提供的二级域名来访问我们的网站了。

绑定域名，以[http://username.github.com]()为例，如果你不想用Github提供的这个二级域名，你也可以绑定自己的域名。具体方法是在仓库根目录下新建一个名为CNAME的文本文件，里面写入你要绑定的域名如：example.com或者blog.example.com。如果要绑定的是顶级域名，则DNS要新建一条A记录，指向204.232.175.78。如果要绑定的是二级域名，则DNS要新建一条CNAME记录，指向username.github.com（请将username换成你的用户名）。到这里，就可以使用example.com或blog.example.com来访问仓库“username.github.com”了，同时也可以用example.com/demo或blog.example.com/demo目录的形式来访问“demo”仓库。

四、使用Markdown写文章并发表
======
Jekyll支持Markdown，这对我们来说是一个好消息。Markdown的目标是实现了「易读易写」的网络的书写语言，具体语法看[这里](http://wowubuntu.com/markdown/)。我们写的一篇文章类似：

	---
	layout: post
	title: Hello Jekyll!
	categories: [Technology]
	tags: [Jekyll, Github, Markdown]
	---
	
	这是H1
	======
	
	- 列表1
	- 列表2
	- 列表3
	
	> 引用
	
	...

然后在命令行下面进入网页项目根目录使用`git`命令进行推送发表。
		
	git add .
	git commit -m "a new post"
	git push origin master(gh-pages)
		
五、问题集锦
======
1. `jekyll --server`在本地测试出现以下错误
	>Liquid error: invalid byte sequencd in GBK
	
	- 临时解决：在执行jekyll命令前，将当前控制台代码格式转换为UTF-8
	
			$export LC_ALL=en_US.UTF-8
			$export LANG=en_US.UTF-8
		
	- 永久解决：把这两个变量添加到操作系统环境变量中。
2. `jekyll --server`时出现编码问题
	>C:/Ruby193/lib/ruby/gems/1.9.1/gems/jekyll-0.12.0/lib/jekyll/convertible.rb:29:in `read_yaml':invalid byte sequence in GBK
	
	- 解决办法：找到ruby目录下gems/jekyll-0.12.0/lib/jekyll/convertible.rb29行修改为下面内容：
			
			self.content = File.read(File.join(base,name),:encoding => "utf-8")
			
3. 每次`git push`都要输入用户名、密码
	- 检查~/.ssh文件夹，看rsa密钥文件是否存在
	- 检查Github控制面板的SSH Keys，看公钥是否添加。
	- 进入命令行切换到项目目录，输入
			git remote -v
		如果显示
		>origin https://...		
		origin https://...
		
		表示没有使用ssh协议，解决办法如下：
			git remote rm origin	#删掉现有仓库地址
			#然后添加使用ssh协议的地址
			git remote add origin git@github.com:username/demo.git
		再次`git push`，不再要求提供密码。
		
4. 怎么删除Github上远程分支？
	由于上述“username.github.com”、“demo”两个仓库要被`push`到特定的分支，操作失误难免会出错，使其出现两个分支。删除远程分支的原理是`push`一个空的项目到该分支上：
	
		remote_repo="https//github.com/username/demo.git"	#这是我想删除分支所在仓库地址
		remote_branch="master"	#这是我想删除分支的名字
		mkdir /tmp/git-empty	#Linux命令，新建名为git-empty文件夹
		cd /tmp/git-empty	#在命令行下切换到该文件夹
		git init #初始化Git
		git push $remote_repo:$remote_branch
			
先到这里，未完待续...




