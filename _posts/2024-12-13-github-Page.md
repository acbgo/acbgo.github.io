---
layout: post
title: 通过GitHub创建个人博客
date: 2024-12-13
author: acbgo
tags: [GitHub, Note]
comments: true
toc: true
pinned: false
---

记录一下如何使用GitHub创建个人博客。

<!-- more -->

## 动机

今天在查找matlab面向对象编程相关资料时进入到博主个人博客主页，看完之后很有收获。
出于好奇，打开作者主页看了一下，发现是通过GitHub Pages搭建的个人博客。
并且记录了很多他在学习过程中的笔记，感觉很有意思。
突然回想自己以前在学习生活中也遇到很多有用的文章或者博客，这些文章成功的帮助了我解决了很多问题。
但是都没有保存记录下来，导致后面再次遇到类似问题时又要重新查找资料。
因此，我也想通过GitHub Pages搭建一个个人博客，记录自己在学习生活中遇到的问题和解决方法。

## 实现
1. 将[作者的仓库](https://zxl19.github.io/)`git clone`到本地；
2. 修改`_config.yml`文件，将对应的信息修改为自己的信息
3. 修改`_posts`文件夹下的文章，将原作者的文章删除，添加自己的内容
4. 修改`image`文件夹下的图片，将原作者的图片删除，添加自己的图片
5. 将修改后的文件`git push`到自己的仓库
6. 在GitHub上设置`GitHub Pages`，（这一步之前已经操作过了，在此不赘述，可以查看网上的众多攻略）

## 后续可新增内容
1. 可参考[博客](https://lemonchann.github.io/blog/create_blog_with_github_pages/#)来添加搜索功能和访问次数统计功能
2. 尝试修改样式等

## 参考
1. [GitHub Pages官方说明](https://pages.github.com/)
2. [一位工程师的存档点](https://zxl19.github.io/)