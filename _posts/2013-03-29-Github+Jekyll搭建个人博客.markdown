---
title: Github+Jekyll搭建个人博客
layout: post

description: 

categories:
  - 前端
  
tags:
  - Jekyll 
  - yaml
  - liquid
  - Github 
  - Blog
 
---


**1. 安装git、ruby**

**2. Github创建Repository，命名必须同下**
	
		${USERNAME}.github.io

**3. 创建Jekyll格式文件目录**

[《Github Pages 及 Jekyll入门》](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

[Jekyll官方文档](http://jekyllrb.com),[中文版](http://jekyll.bootcss.com)

[Jekyll中的YAML](http://jekyllrb.com/docs/configuration/)

[YAML Documnet](www.yaml.org)

[Jekyll中的Liquid](http://jekyllrb.com/docs/variables/)

[Liquid Document](https://docs.shopify.com/themes/liquid-documentation/basics)

**4.Run Jekyll Locally**

	gem install jekyll //安装Jekyll到本地
	jekyll --server	//本地127.0.0.1:4000预览
	
**5.Create a Post**

	rake post[title]

**6.Publish**
	
	git pull origin master //先同步远程文件，后面的参数会自动连接你远程的文件
	git status //查看本地自己修改了多少文件
	git add .//添加远程不存在的git文件
	git commit -m "what I want told to someone"
	git push origin master //更新到远程服务器上
		
**7.更多参考**

[像极客一样写博客](http://zyzhang.github.com/blog/2012/08/29/blogging-like-a-geek/)
[lhzhang的Jekyll博客](http://lhzhang.com)
[林安亚的Jekyll博客](http://painterlin.com)

