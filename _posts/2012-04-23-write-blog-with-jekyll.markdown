---                                                                                                                                                          
layout: post
title: 程序员的写作方式(git + github + jekyll)
category: ruby
---

#What is jekyll?
jekyll是一个轻量级博客系统，也是使用Ruby编写的静态站点生成工具，支持[Markdown](http://zh.wikipedia.org/zh-hans/Markdown)和Texttile标记语言。不同于Wordpress等博客系统，jekyll是纯静态网页的，不需要数据库支持，可以配合第三方服务，例如[disqus](http://disqus.com/)。最关键的是jekyll可以免费部署在Github上，并且可以绑定自己的域名。

#What is Git?
Git是一个开源的分布式版本控制系统，用以有效、高速的处理从很小到非常大的项目版本管理。可以通过[Why
Git is Better than
X](http://zh-cn.whygitisbetterthanx.com/)了解git背后的理念。

#What is github?
GitHub可以托管各种git库，并提供一个web界面，但与其它像
SourceForge或Google
Code这样的服务不同，GitHub的独特卖点在于从另外一个项目进行分支的简易性。为一个项目贡献代码非常简单︰首先点击项目站点的“fork”的按
钮，然后将代码检出并将修改加入到刚才分出的代码库中，最后通过内建的“pull
request”机制向项目负责人申请代码合并。

#Let's Go!
Github的Pages服务可以为每个Github主机上的仓库提供静态页面服务，并且Pages服务支持jekyll。因为Github
Pages有两种Pages，分别是用户页面和项目页面，所以我们可以使用用户页面来创建自己的Blog。

在开始前，请确保你已经有了Github账号一枚和Git的正确配置。没有的朋友可以先移步Github注册并安装配置Git。

首先，创建你的 Blog仓库 `username.github.com`
    $ mkdir username.github.com
    $ cd username.github.com
*Note*：username是你github的用户名。接着新建一个 `index.html` 文件，像下面这样:
	<html>
  		<head>
    			<title>Hello</title>
  		</head>
  		<body>
    			<h1>Hello!</h1>
  		</body>
	</html>

初始化仓库、提交并push到Github:
    $ git init
    $ git add .
    $ git commit -a -m 'init commit.'
    $ git remote add origin
    $ git push origin master

现在你打开 username.github.com
就可以看到刚才新建的页面了，就是这么简单。当然也可以为你的Blog仓库绑定独立域名，具体做法就是：

1. 在你的仓库中新建内容为 www.youdomain.com 的 CNAME 文件；
2. 在你的域名管理页或者是DNS解析的地方，增加一个记录，记录类别为CNAME(Alias)类型.
*Note*：
如果你在CNAME中填写的是顶级域名，就得设置DNS的记录类别为A(Host)型，并设置主机为
207.97.227.245。详细介绍请移步Github的Pages页面。

#Install jekyll
安装jekyll之前请确保你已安装ruby的环境，参考[基于 Ubuntu 11.10 搭建 Ruby on Rails开发环境](http://lightsnail.com/ruby/2012/03/12/build-ruby-on-rails.html)

jekyll的安装很简单，执行：
    gem install jekyll
如果不需要用默认的模版Maruku,想使用RDiscount，则请安装：
    gem install RDiscount
*NOTE*:Maruku是纯ruby的Markdown模版解释器；RDiscount则是c写的模版解释器，后者效率更高。

#Use jekyll
装完jekyll的gem之后，然后运行它，生成一个自己的网站。然后进入自己的jekyll目录，首先配置以下_config.yml文件，指定未来生成的网站的路径以及其他参数。然后运行：

    jekyll --server

关于jekyll的[用法与配置](https://github.com/mojombo/jekyll/wiki/configuration)官方解释很详细,简单认识下jekyll的文件及目录配置:

     .
     |-- _includes
     |-- _plugins 
     |-- _layout 
     |   |-- default.html
     |   |-- post.html
     |-- _post
     |   |-- yyyy-mm-dd-title.markdown
     |   |-- yyyy-mm-dd-title.markdown
     |-- _site
     |-- _config.yml
     |-- index.html

includes存放你需要在模板文件中包含的文件，你可以使用Liquid标签 {‰
include file.ext ‰} 来引用相应的文件。

plugins: 可以增加你自己的插件

layout: 存放布局模板

post: 存放文章列表，文件命名一定要遵循
yyyy-mm-dd-title.html|markdown|textile
规则

site: jekyll自动生成的，所以可以忽略，如果你有在本地安装jekyll并预览了的话，可以使用.gitignore设置Git停止对本目录的跟踪。

config.yml: 设置经常使用的配置选项，这样在本地启动预览时就不用每次都手动输入了。

index.html 和所有的 HTML/Markdown/Textile 文件
所有的HTML/Markdown/Textile文件都可以包含 YAML
配置，这类文件都会被jekyll解析。

#Integrate disqus
由于github page最终生成的都是静态html页面，所以是没有评论功能呢
但我们利用disqus实现在线评论功能，先到 http://disqus.com 注册帐号(免费)
注册成功后，将相应的代码拷贝到post中合适的位置即可。简单起见，只要把
[_includes/post.html](https://github.com/ericshaw/ericshaw.github.com/blob/master/_includes/post.html)
中的ericshaw替换为你的注册帐号就行了(disqus_url输入你实际的域名)

#Integrate rss
因为jekyll可以生成blogs列表，所以我们可以编写atom.xml，由jekyll生成最终xml结果
这是[我的atom.xml文件](https://github.com/ericshaw/ericshaw.github.com/blob/master/atom.xml)

将生成的xml地址提交至 feedsky.com ，由feedsky进行管理和美化

#Quick way
最快的做法是
[fork我的博客](https://github.com/ericshaw/ericshaw.github.com) ，git clone到你的电脑
然后修改成你的，具体需要调整的地方是:

1. 删除_posts中的文章 
2. 按上面介绍的[整合评论]修改 _includes/post.htm 文件
3. 按上面介绍的[整合rss]修改 atom.xml 文件
4. 修改CNAME的内容为你的独立域名
5. 运行jekyll，看看效果
6. 上传!ok，访问你的blog地址看看
