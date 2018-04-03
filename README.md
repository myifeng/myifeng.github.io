# Myifeng

[Myifeng](https://myifeng.github.io) 是一个简洁的博客模板，如果你也喜欢请 Star ，你的 Star 是我持续更新的动力, 谢谢 😄.

### 使用条件

Jekyll 支持 Mac 、Windows、ubuntu 、Linux 操作系统                     
Jekyll 需要依赖：Ruby、bundler

具体版本为:

Rudy:[Ruby 2.2.6](https://dl.bintray.com/oneclick/rubyinstaller/ruby-2.2.6-x64-mingw32.7z)

DevKit:[DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)


#### 安装Jekyll

[Jekyll中文官方文档](http://jekyll.bootcss.com/) ， 如果你已经安装过了 Jekyll，可以忽略此处。

> $ gem install jekyll

#### 获取博客模板

> $ git clone https://github.com/myifeng/myifeng.github.io.git

或者直接[下载博客](https://github.com/myifeng/myifeng.github.io/archive/master.zip)   

进myifeng.github.io/ 目录下，  

开启本地服务前应该首先安装 bundler 

> $ gem install bundler

也可能需要下面这个语句

> $ bundle install

开启本地服务

> $ jekyll server  或者

> $ bundle exec jekyll serve

最后在浏览器输入 [127.0.0.1:4000](127.0.0.1:4000) ， 就可以看到博客效果了。


### 提示

>* 如果你想使用我的模板，请把 _posts/ 目录下的文章都去掉。
>* 修改 _config.yml 文件里面的内容为你自己的个人信息。

如果在部署博客的时候发现问题，可以直接在[Issues](https://github.com/myifeng/myifeng.github.io/issues)里面提问。        


### 把这个博客变成你自己的博客

根据上面【提示】修改过后，在你的github里创建一个username.github.io的仓库，username指的值你的github的用户名。      
创建完成后，把我的这个模板使用git push到你的username.github.io仓库下就行了。
搭建博客如果遇到问题可以看看我教程[使用GitHub+Jekyll搭建个人博客](https://myifeng.github.io)。


#### 感谢   

本博客在[Vno Jekyll](https://github.com/onevcat/vno-jekyll)基础上修改的。  