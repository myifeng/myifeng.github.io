---
layout: post
title: "初识Docker之Docker下安装Oracle"
date: 2018-04-06 
description: "Linux系统中Docker下安装Oracle"
tag: Docker
---  

# **ECS云服务器** #

近期阿里云推出一项优惠政策[1核2G 1M宽带 40G SSD硬盘 的ECS云服务器 99一年 279三年](https://promotion.aliyun.com/ntms/act/group/team.html?group=I00XRrlen0)，当时就很心动，这么好的优惠果断出手，因为不是新用户所以只好借用别人，帮我买了一个一年期的。然后就开始了慢慢配置环境的道路。

# **初识Docker** #

当时买这个服务器主要是为后期的毕业设计做一个部署环境。拿到服务器之后就把JDK、Tomcat、MySQL甚至把Nginx都装了上去。。。顿时有一种全才的赶脚。不过现在手上的很多项目都是使用了Oracle数据库，所以理所当然的要装一个Oracle数据库。

然后网上搜了一堆Linux系统安装Oracle的教程，晦涩难懂，极其复杂。中午问了公司架构师怎么在Linux环境中安装Oracle，然后说出了一个熟悉但从未接触过的名字——Docker。

然后就自己百度Docker相关资料。

>Docker是什么？


    “在一艘大船上，可以把货物规整的摆放起来。并且各种各样的货物被集装箱标准化了，集装箱和集装箱之间不会互相影响。那么我就不需要专门运送水果的船和专门运送化学品的船了。只要这些货物在集装箱里封装的好好的，那我就可以用一艘大船把他们都运走。”

Docker就是类似的理念。现在都流行云计算了，云计算就好比大货轮，Docker就是集装箱。

>安装Docker

Docker 运行在 CentOS 7 上，要求系统为64位、系统内核版本为 3.10 以上。

Docker 运行在 CentOS-6.5 或更高的版本的 CentOS 上，要求系统为64位、系统内核版本为 2.6.32-431 或者更高版本。

在CentOS下使用`yum`安装Docker，一共两行命令：

安装：

>$ yum -y install docker 

启动服务：

>$ service docker start

运行第一个Hello World

>$ sudo docker pull hello-world

>$ sudo docker run hello-word


# **Docker下安装Oracle** #

搜索Oracle镜像

>$ sudo docker search Oracle



    docker.io   docker.io/oraclelinux                         Official Docker builds of Oracle Linux.         434       [OK]
    docker.io   docker.io/frolvlad/alpine-oraclejdk8          The smallest Docker image with OracleJDK 8...   300                  [OK]
    docker.io   docker.io/sath89/oracle-12c                   Oracle Standard Edition 12c Release 1 with...   276                  [OK]
    docker.io   docker.io/alexeiled/docker-oracle-xe-11g      This is a working (hopefully) Oracle XE 11...   240                  [OK]
    docker.io   docker.io/sath89/oracle-xe-11g                Oracle xe 11g with database files mount su...   172                  [OK]
    ......

这里我使用的是`docker.io/sath89/oracle-12c`镜像。

>$ docker pull sath89/oracle-12c

这个镜像有2点多G所以要下载好一会。。。

下载安装之后就可以启动运行Oracle了

>$ sudo docker run -d -p 8091:8091 -p 1521:1521 sath89/oracle-12c

在启动成功之后会显示Oracle运行信息，ID、NAME什么的,这里