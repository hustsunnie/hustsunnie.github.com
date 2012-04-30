---                                                                                                                                                          
layout: post
title: 基于 Ubuntu 11.10 搭建 Ruby on Rails开发环境
category: ruby
---

#目标
搭建一个基于 Ubuntu 11.10 的 Ruby on Rails开发环境，Ruby基于1.9.3版本，Rails基于3.2.0版本。

#第一步：安装Ubuntu
Ubuntu的安装方式不在这里说明，大家可以参照[这篇文章](http://hi.baidu.com/%BD%FC%CE%C0%BE%D1%BB%F7/blog/item/74bf402991738b86033bf69f.html)；  

安装完成后，在Ubuntu中搜索terminal，打开终端，下文所有的命令都在终端输入运行；

安装git、下载、解压与curl、openssl等功能的包：    

    sudo apt-get install build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev autoconf libc6-dev xclip -y
    
    
#第二步：安装RVM
rvm是ruby版本管理器，可以在本机上管理多个不同版本的ruby程序，可通过curl进行安装，命令如下：  

    bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)    
执行以下操作：    

    [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"

#第三步：安装Ruby
    rvm install 1.9.3 
指定系统使用的Ruby版本：  

    rvm use 1.9.3 --default  
测试ruby是否安装成功：   

    ruby -v  
显示版本号，则安装成功

#第四步：安装RubyGems
RubyGems（简称 gems）是一个用于对 Rails 组件进行打包的 Ruby 打包系统。 它提供一个分发 Ruby 程序和库的标准格式，还提供一个管理程序包安装的工具。  

RubyGems的功能类似于Linux下的apt-get。使用它可以方便第从远程服务器下载并安装Rails。  

一般安装完ruby 1.9.3，会自动将rubygems-1.8.17装上，可通过gem -v命令查看版本。如果没有安装，执行以下命令：  

    sudo apt-get install rubygems  

#第五步：安装Rails
通过RubyGems安装rails，执行如下命令：  

    gem install rails -v=3.2.0  
如果显示“ERROR:  Loading command: search (LoadError) no such file to load -- zlib” 错误，则可能是前面的安装有问题，将ruby卸载再重新安装可解决（卸载命令：rvm remove 1.9.3，重新安装：rvm install 1.9.3）。  

#第六步：安装数据库
分别安装mysql和sqlite数据库：

    sudo apt-get install mysql-server mysql-client -y
    sudo apt-get install sqlite3

接着安装对应的RubyGem

    gem install sqlite3-rub
    gem install mysql2

#Ruby开发工具
这里介绍四个比较流行的ruby开发工具：   
           
+ 开源IDE：[netbeans](http://netbeans.org/)  
+ 开源编辑器：[vim](http://www.vim.org/)
+ 商业IDE：[rubymine](http://www.jetbrains.com/ruby/)  

除了以上老牌，还有模仿Mac上的Textmate的替代品是：[Sublime Text](http://www.sublimetext.com),可以提供跨平台的较一致的用户体验。

#异常处理
报错提示：   

    RVM is not a function, selecting rubies with 'rvm use ...' will not work.

解决方法，执行：   

    echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile

然后重启Terminer再执行    

    source .bash_profile






