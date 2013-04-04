---
layout: post
title: "Jekyll Markdown Github Git写blog时的一些小问题与解决办法"
description: ""
categories:
- Web

tags:
- jekyll
- git
- github
- markdown
- question


---
 
在写博客时，用到一些工具Jekyll Markdown Github Git ，几乎都是初次使用，遇到不少问题，这里做个纪录，方便后续查阅，以及深入理解！
 
*   [Git删除文件](#git_rm_file)
*   [使用.gitignore](#git_ignore)
*   [rake a new post](#rake_a_new_post)
*   [插入图片](#insert_picture)
*   [插入多媒体](#insert_media)
*   [Markdown注释功能](#markdown_comments)
*   [Git push error result＝55](#git_error_55)
*   [一键写博客](#one_key_write_blog)

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
  



<h3 id="git_rm_file">
一、Git删除文件
</h3>

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
	
	
<h3 id="git_ignore">
二、使用.gitignore
</h3>

使用Git时，有些文件并不需要上传到Github进行版本跟踪，如，.DS_Store，_sites文件夹等。

在blog目录下，新建文件.gitignore,到里面填写需要过滤的文件或文件夹，如：
		
		_site/*
		_posts/*Question*.markdown
		.DS_Store
		
注意，已上传的文件.gitignore并不会去删除。所以，在新建repo时，要先创建提交.gitignore文件。


<h3 id="rake_a_new_post">
三、rake a new post 
</h3>
新建post，命令如下：

	rake post title=title_name

问题：title_name不支持中文？

在root目录下的rakefile文件中，ENV["title"]表示用户输入的title，做了下面处理,这时rake post title＝title_name 时，就新建了名称是[YY-MM-DD-title_name.markdown]的文件，且写入了YMAL的常规代码。

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
    
其他问题：rakefile 、YMAL、 Liquid 、Jekyll 到底是什么？以后进行进一步理解，争取知道Jekyll运行起来的整个原理！



<h3 id="insert_picture">
四、插入图片
</h3>

####Markdown语法插入图片

	![Chinese Chess](/media/files/2013/02/21/1.png)

####显示效果
![Chinese Chess](/media/files/2013/02/21/1.png)

####HTML代码插入图片

{% highlight html %}
<span class="image-600">![1](/media/files/2013/02/17/1.jpg)</span>
{% endhighlight %}


####显示效果
<span class="image-600">
![1](/media/files/2013/02/21/1.png)
</span>


<h3 id="insert_media">
五、插入多媒体
</h3>
1、插入虾米网音乐
	
	<embed src="http://www.xiami.com/widget/0_1771512762/	singlePlayer.swf" type="application/x-shockwave-flash" 	width="257" height="33" wmode="transparent"></embed>

<embed src="http://www.xiami.com/widget/0_1771512762/singlePlayer.swf" type="application/x-shockwave-flash" width="257" height="33" wmode="transparent"></embed>

2、插入音乐文件

	<embed src="/media/files/2013/03/31/时光.mp3"autostart="false" 	loop="true" width="240" height="40"/>
	
<embed src="/media/files/2013/03/31/时光.mp3" name＝"许巍－时光" autostart="false" loop="true" width="240" height="40" align＝"left" />

3、同样embed可以插入视频


<embed src="http://player.youku.com/player.php/sid/XNDMzNDAzNjQw/v.swf" quality="high" width="480" height="400" align="middle" allowScriptAccess="sameDomain" allowFullscreen="true" type="application/x-shockwave-flash"></embed>


<h3 id="markdown_comments">
六、Markdown注释
</h3>

有时候，用Markdown写的动西，有些临时的想象、突发的灵感，不想展示出来，也不想删除，如何注释呢？

Markdown有没有类似C语言的中的**代码注释**功能呢？既，让有些文字只在编辑页面显示，preview不显示！（好像这个功能是多余的？）

目前我知道的markdown注释文字方法：
	
	~~Strikethrough~~
效果：~~Strikethrough~~。

<h3 id="git_error_55">
七、Git push error result＝55
</h3>

放了一个约7M的音乐文件
	
	git push origin master
时，报下面错误

	RPC failed; result=55, HTTP code = 0

解决办法：

	git config http.postBuffer 524288000	
	git push origin master
	
原因是，上传文件太大，postBuffer默认设置不够。


<h3 id="one_key_write_blog">
八、一键写博客
</h3>
现在用Github 搭建的Jekyll博客，编辑器用Mou，写博客时，有下面几个重复步骤：

	1、terminal到Blog的root目录。

	2、rake post title=title_name来Create a new post .

	3、Markdown打开title_name，开始编写。

	4、jekyll --server，打开safari访问localhost：4000运行预览。

能否，一键完成1到3操作，直接进入编辑。然后一键运行4，显示预览结果呢？  

用到，Automator ？AppleScript？Cocoa ？或是其他实现方法？

**有待进一步解决！**






