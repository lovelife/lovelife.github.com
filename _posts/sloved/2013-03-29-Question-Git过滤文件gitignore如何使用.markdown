---
title: Question-Git过滤文件gitignore如何使用
layout: post

description: "Git 文件过滤配置.gitignore"

categories:
  - Git
  
tags:
  - git
  - question
  
---

在使用Jekyll时，有些文件并不需要上传到服务器进行版本跟踪，如，.DS_Store，_sites文件夹等。
在目录下，新建文件.gitignore,到里面填写需要过滤的文件或文件夹即可。如：
		
		_site
		post_example/*.*
		_posts/*Question*.markdown
		.DS_Store
		
注意，在新建repo时，要先创建提交.gitignore文件，否则，文件已传上去后再设置.gitignore并不会删除已存在服务器上的文件。	
