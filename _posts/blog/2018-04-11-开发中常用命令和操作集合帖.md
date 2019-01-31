---
layout: post
title: "开发中常用命令和操作集合帖"
categories: command
date: 2018-04-15 
description: "命令集合帖"
keywords: command
---  

# 前言

此贴只为记录日常使用的一些常用命令或者一些操作，仅作为日常笔记而已，好记性不如烂笔头。日常更新。

# Java

> 递归判断编号，根据增长生成不重复编号

    public String checkApplyNo(String applyNo) {
		List<String> list = dao.queryApplyNo(applyNo);
		if (list != null && list.size() > 0) {
			return checkApplyNo(String.valueOf(Long.valueOf(applyNo) + 1));
		}
		return applyNo;
	}


# Linux

> ps -ef|grep tomcat  显示所有Tomcat进程信息



# EasyUI

##

> jQuery 选择器



> $(".class").css("display","none");  //设置不显示

> $(".class").css("display","");  //设置显示

> $("#id").textbox({required:false,value:''});//设置必填，赋值

