---
layout: post
title: "Git push error result=55"
description: ""
categories:
- web

tags:
- git
- question


---

放了一个约7M的音乐文件，git push origin master时，报下面错误

	RPC failed; result=55, HTTP code = 0

解决办法：

	git config http.postBuffer 524288000	
	
原因是，postBuffer默认设置不够。

参考：
[1] http://stackoverflow.com/questions/11968353/cannot-push-to-remote-git-repository