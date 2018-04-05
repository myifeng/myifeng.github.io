---
layout: post
title: "使用GitHub+Jekyll搭建个人博客"
date: 2018-04-01 
description: "Jekyll配置，Jekyll+Github，搭建自己的博客"
tag: 博客
---   

　　去年刚接触GitHub时，出于好奇，利用GitHub+HEXO搭建了一个自己的个人主页。整个过程崎岖坎坷，不过最后也是成功啦。后来由于学习和工作原因，加上更换电脑环境丢失，也就更新了几篇就停更了。
　　最近突然想到这件事，决定把环境配上重新创建一个个人主页。这个决定采用现在比较流行的GitHub+Jeky来搭建。
　　
# **Jekyll** #
    
&ensp;&ensp;&ensp;&ensp;Jekyll是一个简单的免费的Blog生成工具，类似WordPress。但是和WordPress又有很大的不同，原因是jekyll只是一个生成静态网页的工具，不需要数据库支持。但是可以配合第三方服务,例如Disqus。最关键的是jekyll可以免费部署在Github上，而且可以绑定自己的域名。

&ensp;&ensp;&ensp;&ensp;了解了Jekyll是什么，下面就开始步入正题，开始搭建个人主页。
　　
# **安装Ruby** #

&ensp;&ensp;&ensp;&ensp;首先下载[Rulby](https://rubyinstaller.org/downloads/ "Ruby")安装包。

&ensp;&ensp;&ensp;&ensp;这里我一开始下载的是2.5.1版本，在后期运行Jekyll时报错，后来降低了版本，安装了2.2.6版本，就运行正常了，所以推荐使用2。0~3.0之间的版本。

![](https://i.imgur.com/plTy6wX.png)

&ensp;&ensp;&ensp;&ensp;安装时勾选第二项“Add Ruby executables to your PATH”,选定安装目录，例如`D:\Ruby22-x64`,等待安装结束。

&ensp;&ensp;&ensp;&ensp;打开cmd控制台，输入`ruby -v`，如出现版本信息，则安装成功。我的输出为`ruby 2.2.6p396 (2016-11-15 revision 56800) [x64-mingw32]`

# **安装Devkit** #


&ensp;&ensp;&ensp;&ensp;下载[Devkit](https://rubyinstaller.org/downloads/ "Devkit")安装包，我安装的是`DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe`

&ensp;&ensp;&ensp;&ensp;下载完成后双击解压到制定目录下，例如：`D:\Devkit`.

## 初始化DevKit ##


&ensp;&ensp;&ensp;&ensp;在Deckit解压目录运行cmd，执行`ruby dk.rb init`，初始化成功后，Devkit目录下将出现`config.yml`文件，打开，最后有一句`- D:\Ruby22-x64`（这里是Ruby的安装目录），如没有，则手动添加。

&ensp;&ensp;&ensp;&ensp;回到cmd窗口，继续执行`ruby dk.rb install`，顺利结束后，则Devkit配置完成。

# **安装Jekyll** #


cmd运行`gem install jekyll`，顺利结束后，输入`jekyll -v`检测是否安装成功。

使用`jekyll new myblog`新建一个博客，`cd myblog`打开该目录，运行`jekyll s / jekyll serve`运行该博客，即可在浏览器预览该博客。地址为：127.0.0.1:4000。

如在启动时报错，可能是因为缺少 `bundler`

可以尝试安装 bundler ：

> $ gem install bundler

也可能需要下面这个语句

> $ bundle install

我这里是两个命令都执行了才顺利启动的。

# **问题** #

在安装和运行过程中遇到了很多问题，有些问题现在仍然没有解决，比如评论功能和分享功能。

评论功能计划是用[友言](http://www.uyan.cc/)做的，不知道为什么放上去就是不显示评论框，可能是配置问题吧；另一个就是分享功能，使用了两种插件都不好用，一个是[百度分享](http://share.baidu.com/)，一个是[JisThis](http://www.jiathis.com/),本地运行正常，到了线上就不能显示，调测了一下，是因为现在我这个博客访问是用的https，而这两款插件访问都是http请求，不知道是不是这个问题，所以这两个功能模块就暂时搁置了。

如果你有好的方式或者解决方法，欢迎给我提[Issue]([Issues](https://github.com/myifeng/myifeng.github.io/issues))，万分感激。