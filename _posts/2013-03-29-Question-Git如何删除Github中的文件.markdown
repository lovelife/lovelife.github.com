
---
layout: post
title: "Question-Git如何删除文件"

categories:
- Tools

tags:
- git
- github
- question


---

初使用，还没熟悉、习惯、理解git工具。删除文件操作出现下面问题。

####git如何删除文件

我Github lovelife.github.com上_posts文件夹下的很多文件需要删除.
如何在本地通过命令来执行？

尝试：

	git rm file
	git push origin master

似乎只是把本地的删除了，已经在服务器上的无法删除。

解决：

	git rm file
	git commit -m "rm file"
	git push origin master
	
####还是git删除文件

我想删除文件file,第一反应是手动删除（而不是git rm file），然后提交到Github：
	
	git status
	git add .
	git commit -m "rm file"
	git push origin master
	
结果，Github上的对应文件并**没有**删除！怎么回事？最后改成下面commit方式，达到想要的效果了：

	git commit -a -m "rm file"
	

	