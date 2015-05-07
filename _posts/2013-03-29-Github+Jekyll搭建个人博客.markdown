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
  - git
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

**8.问题与解决**

在写博客时，用到一些工具Jekyll Markdown Github Git ，几乎都是初次使用，遇到不少问题，这里做个纪录，方便后续查阅，以及深入理解！

* [ ][使用.gitignore](#git_ignore) 
* [x][Git删除文件](#git_rm_file)
* [x][rake a new post](#rake_a_new_post)
* [x][插入图片](#insert_picture)
* [x][插入多媒体](#insert_media)
* [x][Markdown注释功能](#markdown_comments)
* [x][Git push error result＝55](#git_error_55)
* [ ][一键写博客](#one_key_write_blog)
* [x][超链接](#hyper_link)

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
  
<h4 id="git_ignore">
使用.gitignore
</h4>

使用Git时，有些文件并不需要上传到Github进行版本跟踪，如，.DS_Store，_sites文件夹等。

在blog目录下，新建文件.gitignore,到里面填写需要过滤的文件或文件夹，如：
		
		_site/*
		.DS_Store
		
注意，已上传的文件.gitignore并不会去删除。所以，在新建repo时，要先创建提交.gitignore文件。

那如果是一堆文件夹，我只有一个要同步，其他全部ignore呢？怎么处理？


<h4 id="git_rm_file">
Git删除文件
</h4>

需求：我Github repo lovelife.github.com 上_posts目录下有些文件要删除，怎么处理？

先从本地删除file，然后push到Github上的分支上，尝试下面操作即可：
	
	 git rm file
	 git commit -m "rm file"
	 git push origin master
	 
另外，在删除file时，我第一反应是通过手动直接删除（而不是git rm file）,然后push到Github时，总是不能成功，不能删除Github上对应存在的文件，尝试下面操作即可：

	git status
	git add .
	git commit -a -m "rm file"
	git push origin master 
	
	



<h4 id="rake_a_new_post">
rake a new post 
</h4>
新建post，命令如下：

	rake post title=title_name

问题：title_name不支持中文？

在root目录下的rakefile文件中，ENV["title"]表示用户输入的title，做了下面处理,这时rake post title＝title_name 时，就新建了名称是[YY-MM-DD-title_name.markdown]的文件，且写入了YMAL的常规代码。

```ruby
	# Usage: rake post title="A Title" [date="2012-02-09"]
	desc "Begin a new post in #{CONFIG['posts']}"
	task :post do
	abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
	
	#获得标题
	title = ENV["title"] || "new-post"
	time = Time.now
	filename = "_posts/" + time.strftime("%Y-%m-%d-") + title + '.markdown'
	
	if File.exists? filename then
    	abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
    end
    puts "Creating new post: #{filename}"
    
    open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "description: \"\""
    post.puts "categories:"
    post.puts "- "
    post.puts "tags:"
    post.puts "- "
    post.puts ""
    post.puts ""
    post.puts "---"
    end #do
    end # task :post
```
    
    
其他问题：rakefile 、YMAL、 Liquid 、Jekyll 到底是什么？以后进行进一步理解，争取知道Jekyll运行起来的整个原理！



<h4 id="insert_picture">
插入图片
</h4>

####Markdown语法插入图片

	![Chinese Chess](/media/files/2013/02/21/1.png)

####显示效果
![Chinese Chess](/media/files/2013/02/21/1.png)

####HTML代码插入图片

```html
<span class="image-600">![1](/media/files/2013/02/17/1.jpg)</span>
```


####显示效果
<span class="image-600">
![1](/media/files/2013/02/21/1.png)
</span>


<h4 id="insert_media">
插入多媒体
</h4>
1、插入虾米网音乐
	
	<embed src="http://www.xiami.com/widget/0_1771512762/	singlePlayer.swf" type="application/x-shockwave-flash" 	width="257" height="33" wmode="transparent"></embed>

<embed src="http://www.xiami.com/widget/0_1771512762/singlePlayer.swf" type="application/x-shockwave-flash" width="257" height="33" wmode="transparent"></embed>

2、插入音乐文件

	<embed src="/media/files/2013/03/31/时光.mp3"autostart="false" 	loop="true" width="240" height="40"/>
	
<embed src="/media/files/2013/03/31/时光.mp3" name＝"许巍－时光" autostart="false" loop="true" width="240" height="40" align＝"left" />

3、同样embed可以插入视频


<embed src="http://player.youku.com/player.php/sid/XNDMzNDAzNjQw/v.swf" quality="high" width="480" height="400" align="middle" allowScriptAccess="sameDomain" allowFullscreen="true" type="application/x-shockwave-flash"></embed>


<h4 id="markdown_comments">
Markdown注释
</h4>

有时候，用Markdown写的动西，有些临时的想象、突发的灵感，不想展示出来，也不想删除，如何注释呢？

Markdown有没有类似C语言的中的**代码注释**功能呢？既，让有些文字只在编辑页面显示，preview不显示！（好像这个功能是多余的？）

目前我知道的markdown注释文字方法：
	
	~~Strikethrough~~
效果：~~Strikethrough~~。

<h4 id="git_error_55">
Git push error result＝55
</h4>

放了一个约7M的音乐文件
	
	git push origin master
时，报下面错误

	RPC failed; result=55, HTTP code = 0

原因是，上传文件太大，postBuffer默认设置不够。解决办法：

	git config http.postBuffer 524288000	
	git push origin master
	
	

<h4 id="one_key_write_blog">
一键写博客
</h4>
现在用Github 搭建的Jekyll博客，编辑器用Mou，写博客时，有下面几个重复步骤：

	1、terminal到Blog的root目录。

	2、rake post title=title_name来Create a new post .

	3、Markdown打开title_name，开始编写。

	4、jekyll --server，打开safari访问localhost：4000运行预览。

能否，一键完成1到3操作，直接进入编辑。然后一键运行4，显示预览结果呢？  

用到，Automator ？AppleScript？Cocoa ？或是其他实现方法？


<h4 id="hyper_link">
超链接使用
</h4>

	[Love](/media/files/2013/03/30/lovelife.jpg)
	[Unix](/media/files/2013/04/05/Unix四十年.pdf)
	
[Love](/media/files/2013/03/30/lovelife.jpg)
[Unix](/media/files/2013/04/05/Unix四十年.pdf)	

