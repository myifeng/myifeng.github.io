---
layout: post
title: "Java企业级电商项目架构演进之路"
categories: 架构
date: 2018-04-21 
description: "Tomcat集群及Redis分布式"
keywords: 架构
---   

# **目录** #

- [1.开篇](#1.开篇)
	- [1.1 前言]()
    - [1.2 大型Java项目架构演进解析](#1.2)
- [2.Lombok框架集成及原理解析](#2)
	- [2.1 Lombok简介]()
	- [2.2 Lombok的原理]()
	- [2.3 Lombok的使用]()
	- [2.4 总结]()      

<!-- /TOC -->

# **1 开篇** #


##1.1 前言

![](https://i.imgur.com/JcJI1eC.png)

本文基于一个完整电商项目进行架构演进，覆盖Tomcat集群+Nginx负载均衡+Redis分布式等核心技能点。

##1.2 大型Java项目架构演进解析

任何一个系统的架构都不是一蹴而就的，都是在经历过各种升级迭代之后，各种优化，各种调整之后的产物。例如：一个简单的单服务架构，系统由一个服务器应用和一个数据库加上一个文件服务器构成，通过一个Nginx进行转发。

![](https://i.imgur.com/w3zaykx.png)

在随着系统用户量的不断提高，对系统也提出了更高的要求，从而就产生了下面这种服务器集群的架构。

![](https://i.imgur.com/1aQVjXq.png)

然后架构在逐渐升级，逐渐完善，就有了下面的服务器集群和分布式缓存系统架构。

![](https://i.imgur.com/Uk7GQQt.png)

当然随着用户的增多，数据库和文件服务器肯定也会做集群，来满足业务场景的需要。

# **2 Lombok框架集成及原理解析** #

##2.1 Lombok简介

Lombok是一个可以通过简单的注解形式来帮助我们简化消除一些必须有但显得很臃肿的Java代码的工具，通过使用对应的注解，可以在编译源码的时候生成对应的方法。

例如：我们平时开发过程中总是要花很多时间为Java Bean去创建getter和setter方法，当类里面的属性很多时则创建的getter和setter就很多，代码就很长。而lombok就可以为我们省去创建getter和setter方法的麻烦，代码也会更加简洁。

Lombok官方地址: [www.projectlombok.org](www.projectlombok.org "www.projectlombok.org")

##2.2 Lombok的原理

接下来进行lombok能够工作的原理分析。 
自从Java 6起，javac就支持“JSR 269 Pluggable Annotation Processing API”规范，只要程序实现了该API，就能在javac运行的时候得到调用。 
举例来说，现在有一个实现了"JSR 269 API"的程序A,那么使用javac编译源码的时候具体流程如下： 
1)javac对源代码进行分析，生成一棵抽象语法树(AST) 
2)运行过程中调用实现了"JSR 269 API"的A程序 
3)此时A程序就可以完成它自己的逻辑，包括修改第一步骤得到的抽象语法树(AST) 
4)javac使用修改后的抽象语法树(AST)生成字节码文件 

![](https://i.imgur.com/BlXjt0w.jpg)


##2.3 Lombok的使用

如果是使用Maven构建项目，则添加以下依赖：

    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.16.18</version>
        <scope>provided</scope>
    </dependency>


否则直接下载jar包并引入到项目中，下载地址[www.projectlombok.org/download](https://projectlombok.org/download)


lombok的使用主要是通过注解方式。


	@Getter
	@Setter
	@ToString
	@EqualsAndHashCode（of={"userName","passWord"}）
	@NoArgsConstructor
	public class User{
		private String userName;
		private String passWord;
	} 


`@Getter`/`@Setter` 

用于生成getter和setter方法。例如：

`userName` 和 `passWord`在编译时都会生成getter和setter方法，生成的getter和setter方法是`public`的；若要修改其修饰符可设置`AccessLevel的值`，如`passWord`的getter方法就是`private`。

`@Getter`/`@Setter`可以直接在类上进行注释，对类里面所有的属性均可生成getter和setter方法，


`@ToString`

使用`@ToString`会生成`toString()`方法，它会按顺序依次打印类名、字段；若想忽略输出字段，则可以用`exclude`设置参数；如果有继承父类，可以设置`callSuper`为`true`让其调用父类`toString()`方法：

`@EqualsAndHashCode`

使用@EqualsAndHashCode会生成hashCode()和equals()方法，默认会使用所有非静态、非transient字段；
如果想排除某些字段可设置exclude参数；
如果想指定某些字段可设置of参数；
如果有继承父类，可以设置callSuper为true让其调用父类生成的equals()和hashCode方法，但是当没有继承父类并设置callSuper为true时会在编译时报错。

`@NoArgsConstructor`

使用`@NoArgsConstructor`生成一个无参数构造函数。

`@AllArgsConstructor`

生成全参数构造函数，将类中的每个字段生成带有1个参数的构造函数，例如有3个字段，则构造函数的参数为3个;

`@Data`

`@Data`包含了`@ToString`, `@EqualsAndHashCode`,`@Getter`, `@Setter`, `@RequiredArgsConstructor`的功能。

更多注解、用法和说明可查看官网文档[Lombok features](https://projectlombok.org/features/all)

##2.4 总结

使用lombok能够为我们省去手动创建getter和setter方法的麻烦，lombok 有助于代码的整洁、效率的提高以及冗余的减少，但也同时降低了源代码文件的可读性和完整性。

不可过度依赖lombok。


 