---
layout: post
title: "使用Docker搭建GitLab"
categories: Docker
date: 2019-02-01 
description: "Linux系统中Docker下安装GitLab,搭建自己的版本控制"
keywords: Docker
---  

[GitLab](https://about.gitlab.com/) 是一个用于仓库管理系统的开源项目。使用Git作为代码管理工具，并在此基础上搭建起来的web服务。

可通过Web界面进行访问公开的或者私人项目。它拥有与Github类似的功能，能够浏览源代码，管理缺陷和注释。可以管理团队对仓库的访问，随着git的流行，越来越多的技术团队通过在自己的服务器搭建gitlab来实现代码的管理。

现在我们在Linux系统下，通过Docker进行搭建自己的一个GitLab私服。

## 1.搜索镜像 

首先通过 `docker search gitlab` 搜索 gitlab 镜像；

![](/images/blog/2019-02-01-1.png)

这里的 docker.io/gitlab/gitlab-ce 是 GitLab 官方的镜像，我们使用这个。

## 2.下载镜像

使用 `docker pull gitlab/gitlab-ce` 下载镜像；

下载完成后，通过 `docker images` 查看当前系统所有的镜像；

![](/images/blog/2019-02-01-2.png)

## 3.创建并启动容器

然后就可以通过

```
docker run -d -h gitlab -p 443:443 -p 8085:80  -p 2222:22 
--name gitlab --restart always  
-v /root/data/gitlab/config:/etc/gitlab 
-v /root/data/gitlab/logs:/var/log/gitlab 
-v  /root/data/gitlab/data:/var/opt/gitlab  docker.io/gitlab/gitlab-ce
```

创建并启动容器，这里将端口和文件映射到本机，吧文件映射到本机这是非常重要的。

## 4.绑定域名

然后我们将域名 `git.domain.com` 通过 nginx 指向8085端口，重启 nginx 生效。

好像最后还要通过

`docker exec -t -i gitlab vim /etc/gitlab/gitlab.rb`

或者

`vim /root/data/gitlab/config/gitlab.rb`

修改 `gitlab.rb`文件

```
external_url "http://git.domain.com"
```

这里配置的是之前 nginx 绑定的域名。

之后 `docker restart gitlab` 重启容器；

## 5.修改root密码登录

访问`git.domain.com`,首次访问可能会有问题，多刷新几次，即可看到更新密码，这里是为root用户修改密码，修改完成之后即可通过root用户登录。

![](/images/blog/2019-02-01-3.png)

![](/images/blog/2019-02-01-4.png)


## 6.大功告成！

这样我么那就搭建了一个自己的代码管理仓库，可以尽情使用！
