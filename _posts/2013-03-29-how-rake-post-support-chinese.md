---
layout: post
title: "如何使Jekyll rake a post 时title支持中文"

description: Jekyll rake post title 中文的支持

categories:
- Web

tags:
- jekyll
- rake
- question


---

####问题描述
用jekyll写博客时，通过下面命令创建文档
	
	rake post title="title_name"
	
其中title_name不能有空格，不能有中文。那么如何使得title_name支持中文呢？

####解决方法
在blog目录下的Rakefile文件中,rake post title 函数中，ENV["title"]就是接收所输入的字符，直接使用即可!

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
	
	