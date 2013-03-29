---
layout: post
title: "如何使Jekyll rake a post 时支持中文"

description: Jekyll rake post title 中文的支持

categories:
- Web

tags:
- jekyll
- rake
- question


---

###问题描述
用jekyll写博客时，通过下面命令创建文档
	
	rake post title="title_name"
	
或者

	rake post["title_name"]
	
其中title_name不能含有空格，也不能有中文。那么如何使得title_name支持中文呢？

###解决方法
		