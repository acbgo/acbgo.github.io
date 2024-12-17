---
layout: post
title: 微信自动化解析信息初步尝试（一）
date: 2024-12-13
author: acbgo
tags: [微信, 自动化]
comments: true
toc: true
pinned: false
---
通过python自动化解析联系人信息的初步尝试

<!-- more -->

### 动机
最近和朋友吐槽目前市场上已有的记账软件过于难用，有时候我只是需要一些简单的功能，
但是市面上的软件功能过于冗余。在小红书上面检索发现了一个叫做[翻身喵](oc1.cn)的记账工具，功能简单，界面简洁: [小红书链接](https://www.xiaohongshu.com/discovery/item/6756d6520000000002017ab5?source=webshare&xhsshare=pc_web&xsec_token=AB27uVupQNqH5sDksT0M1pz8ed58H5hC7f1j3LDPK3ih4=&xsec_source=pc_share)

其通过通过微信公众号+前后端网页式实现，实现过程如下：
- 关注“翻身猫记账”服务号
- 将记账信息发送给该服务号
- 服务号后台对记账信息进行处理并返回对应的个人链接（后台采用何种方式实现未知）
- 点击链接即可查看个人账户的记账信息 


因此打算借助这个思路，实现一个自动微信记账助手，实现类似的功能，理想状态下的功能和步骤如下：
- 通过代码登录小号微信
- 配置文件设定某个好友微信ID，当收到该好友信息时，解析收到的信息
- 如果是记账信息，则处理后以某种格式储存到文本文件中，并返回当前记账汇总
- 用户可以发送特定指令查询汇总信息或者生成图片返回等。

为什么要重新开发一个而不是直接使用翻身喵呢？有以下几个原因： 
1. 翻身喵目前处于起步阶段，功能尚未完全开发完毕，商业化计划未知，不知道未来是否会对一些功能进行收费。如果前期投入使用之后，形成依赖，后期收费可能会受到影响并产生不必要的费用。
2. 不确定翻身喵能否持续运营，如果经营不善，入不敷出，无法支付服务器续费费用而运营不下去，那么之前的记账信息可能会丢失。
3. 通过自己开发，可以实现高度的自定义，可以根据自己的需求进行功能扩展，比如可以实现文本导出、图片导出、数据分析等功能。

### 实现
现实总是残酷的，经过一番检索和尝试，发现微信官方并没有提供类似的API，在GitHub上找到一些相关的开源库，
比如[itchat](https://github.com/littlecodersh/ItChat)和[wxpy](https://github.com/youfou/wxpy)但是都是基于web微信的，
其中itchat库的实现是基于网页版微信的，而wxpy库是基于itchat库进行二次开发的，但是由于微信官方对网页版微信的限制，
这两个库目前都无法再继续使用了。以下两篇文章对此有详细的介绍：
1. [再也不见，Itchat！](https://blog.csdn.net/qq_43573112/article/details/125822731)
2. [再见，itchat！再见，网页版微信！](https://blog.csdn.net/wade1203/article/details/107010918)

但是也比较幸运找到了一些可以用的代码库，如[wxauto](https://github.com/cluic/wxauto)，
这个库是Windows版本微信客户端（非网页版）的自动化，可实现简单的发送、接收微信消息，简单微信机器人等功能
笔者通过安装这个库并进行了一番实践，发现实际效果与预期的相差甚远。其实现过程大概如下：
- 先在Windows登录微信客户端
- 运行写好的代码，调用对应的方法，比如向文件传输助手发送一条消息
- 代码拉起微信页面，查找对应的好友，通过点击好友头像进入聊天界面，然后发送消息

这种方式确实可以实现发送信息，但是这些任务都是在前台执行的，无法实现后台自动化，而且代码运行时会弹出微信页面。
这种实现方式对于笔者的需求来说并不是很友好，并且不如翻身喵的实现来得优雅。因此决定暂时放弃这个库，继续寻找其他的解决方案。

在文献1中，作者提到了几个其他的开源代码库：等有时间了再一一进行分析和尝试
1. [WeChatPYAPI](https://github.com/mrsanshui/WeChatPYAPI)
2. [wxBot](https://github.com/liuwons/wxBot)
3. [wechaty](https://github.com/wechaty/wechaty)
4. [Mojo-Weixin](https://github.com/hexsum/Mojo-Weixin)
5. [vbot](https://github.com/hanson/vbot)
6. [itchat4j](https://github.com/yaphone/itchat4j)
7. [jeeves](https://github.com/kanjielu/jeeves)
8. 另外文献1的评论区中有人提到itcha依旧可以使用，这个也需要进一步验证。
9. [wechat-bot](https://github.com/cixingguangming55555/wechat-bot)


###### 另外笔者还尝试了像翻身喵一样注册服务号来使用，发现微信公众号有两种，分别是订阅号和服务号，但是服务号需要企业资质才能注册，订阅号不确定能否实现同样的功能，仍需进一步验证。
