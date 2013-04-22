---
layout: post
title: "Question-jekyll blog 插入音频"

categories:
- Web

tags:
- music
- jekyll
- html
- question
- markdown


---

###问题
用jekyll,markdown写博客，如何插入音乐？

1、插入虾米网音乐
	
	<embed src="http://www.xiami.com/widget/0_1771512762/	singlePlayer.swf" type="application/x-shockwave-flash" 	width="257" height="33" wmode="transparent"></embed>

<embed src="http://www.xiami.com/widget/0_1771512762/singlePlayer.swf" type="application/x-shockwave-flash" width="257" height="33" wmode="transparent"></embed>

2、插入音乐文件

	<embed src="/media/files/2013/03/31/时光.mp3"autostart="false" 	loop="true" width="240" height="40"/>
	
<embed src="/media/files/2013/03/31/时光.mp3" name＝"许巍－时光" autostart="false" loop="true" width="240" height="40" align＝"left" />

3、同样embed可以插入视频


<embed src="http://player.youku.com/player.php/sid/XNDMzNDAzNjQw/v.swf" quality="high" width="480" height="400" align="middle" allowScriptAccess="sameDomain" allowFullscreen="true" type="application/x-shockwave-flash"></embed>

