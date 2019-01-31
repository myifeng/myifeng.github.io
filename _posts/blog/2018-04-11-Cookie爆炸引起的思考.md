---
layout: post
title: "Cookie爆炸引起的思考"
categories: Cookie,JQuery
date: 2018-04-11 
description: "Cookie爆炸引起的思考"
keywords: Cookie,JQuery
---  

# **Cookie大爆炸** #

“页面加载不出来了！！！，又出现一个BUG”

测试系统登陆之后加载不出来，所有页面都挂掉了，但是有的用户登录却很正常。两者对比发现登录后异常的账号是最近用来开发新模块用的账户，所以紧急排查了一下新开发的功能模块，并没有发现问题。并且登录正常的用户也有这个新开发的模块，所以问题应该不是出在新开发的模块上，应该是登录时候哪里出现了问题。

登录时访问后台成功，所以问题极有可能出在登陆之后的操作——Cookie的操作中。因为在登陆之后，要将后台返回过来的相关信息放入Cookie中，后来删掉跟新功能有关的那个Cookie操作，果然就正常了。

问题的原因是什么呢？既不是新功能模块的原因，也是不是新功能操作Cookie的原因，而是Cookie的值过大引起的。在登录异常的用户的Cookie一共有8700字符，删掉没有Cookie之后只有4500多字符，然后系统就正常了。可见Cookie虽好，可不要贪多啊！

到底各种浏览器对Cookie的限制大小为多少，网上也是说法不一，截取了一个，但是感觉应该描述不准确，至少现在我用的Chrome，Cookie4500多字节依然没有问题。


|           | IE6.0    | IE7.0+     |  Opera    | FF        | Safari    | Chrome    |
| --------  | -----:   | :----:     | :----:    | :----:    | :----:    | :----:    |
|cookie个数 |每个域为20个|每个域为50个|每个域为30个|每个域为20个|没有个数限制|每个域为53个|
|cookie大小 |4095个字节 |4095个字节  |4096个字节  |4097个字节  |4097个字节 |4097个字节  |

# **JQuery操作Cookie** #

    $.cookie('the_cookie','the_value',{
        expires:7,  
        path:'/',
        domain:'jquery.com',
        secure:true
    })

    expires：（Number|Date）有效期；设置一个整数时，单位是天；也可以设置一个日期对象作为Cookie的过期日期；
    path：（String）创建该Cookie的页面路径；
    domain：（String）创建该Cookie的页面域名；
    secure：（Booblean）如果设为true，那么此Cookie的传输会要求一个安全协议，例如：HTTPS；


1.增加一个Cookie

> $.cookie('the_cookie', 'the_value');

2.创建一个cookie并设置有效时间为7天

> $.cookie('the_cookie', 'the_value', { expires: 7 });

3.创建一个cookie并设置cookie的有效路径

> $.cookie('the_cookie', 'the_value', { expires: 7, path: '/' });

4.读取cookie

> $.cookie('the_cookie');

5.删除cookie

> $.cookie('the_cookie', null);


