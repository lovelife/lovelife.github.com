---
layout: post
title: "一键运行Jekyll并rake a new post打开Markdown进入编辑"
description: "一键运行Jekyll并rake a new post打开Markdown进入编辑"

categories:
- Mac
- Web

tags:
- automator
- appleScript
- jekyll
- question


---

####问题
每次用markdown写博文时，总是先打开Terminal，cd到blog目录，然后rake post title = new post。

若要查看效果，同样要在blog下打开Terminal，执行jekyll --server ,然后打开浏览器localhost:4000查看效果。

若每天都写东西，每天都进行这样重复性的操作，很嫌麻烦，能否自动化呢？

####需求
基本需求1 ：点击app1,输入title,自动rake a post ,并用Markdown打开对应文档，相当于一键我就可以进行编辑了！

高级需求，点击app1,可以浏览以往的post.

基本需求2：点击app2 , 可以直接打开浏览器预览localhost:4000。


####实现

1、automator + applescript ?

2、object c ?