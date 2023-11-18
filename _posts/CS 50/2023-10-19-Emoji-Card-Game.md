---
title: 打造一款iOS小游戏，Emoji Card Game---CS50 Final Project(swift, ios)
author: mordecaimaic
date: 2023-10-19 19:17:03 +0800
categories: [CS自学, CS50]
tags: [cs50]     # TAG names should always be lowercase
---
# CS50 Final Project
这是我的第一款iOS应用，可以先看看效果图
首先可以看一下[我的final project视频介绍](https://www.youtube.com/watch?v=tZj4Tcr7Qyc)，非常朴素的一个小游戏。
下面是效果图

![emoji_card_game_0](/assets/images/cs50/cs50_final_project_emoji_card_game_0.png){: .w-25}


首先可以看一下[我的final project视频介绍]，非常朴素的一个小游戏，
## Video

{% include embed/youtube.html id='tZj4Tcr7Qyc' %}

cs50的final project是自由的，因此我们挑选一些我们喜欢的主题来进行制作，老师给了我们推荐一些可以自由发挥的选题，让我们来看看老师给我们推荐的一些选题。
- a web-based application using JavaScript, Python, and SQL
- an iOS app using Swift
- a game using Lua with LÖVE
- an Android app using Java
- a Chrome extension using JavaScript
- a command-line program using C
- a hardware-based application for which you program some device

大概的意思就是
- 一款使用JavaScript, Python 和SQL的web应用
    >这个和finance的作业基本一样，打造一个模拟股票购买的页面，但是我js的语法还不是很熟练，只是在week-8稍微使用过一点
- 一款使用swift语言构造的iOS app
    >我选择了这个作为我的final project，下面会仔细介绍。
- 一款使用使用Lua语言打造的love游戏
    >之前听说过Lua，之前只是知道Lua是一个脚本语言。但是不知道Lua原来是用来制作一些游戏的，有时间可以尝试玩一下
- 一款使用Java打造的安卓app
    >这个非常经典了，安卓app，需求量应该非常大
- 一款用Javascript打造的chrome扩展应用
    >我每天都在使用别人制作的chrome的扩展应用，包括我的uBlock Origin(chrome广告拦截器)，以及我的Youtue双字幕扩展应用。
    但是我还没有自己写过扩展应用。有时间也可以尝试一下
- 一款使用C语言打造的命令行程序
    > 这个也非常经典了，前几章在cs50做过不少类似这种，比如打开文件，操作文件，对图像进行模糊，滤镜等。也可以有各种各样不同的算法数据结构等，例如投票竞选人；哈希字典等（有时间的话会开一个新的博客，稍微重新复习一下cs50前面的内容）
- 一些基于硬件的应用（给一些设备进行编程）
    > 这不就是我这个学期要做的raspberry和fpga吗？？？🤔️

看了这么多的推荐，我感觉我好像一直很想做一款iOS的应用，在mac上使用xcode对编写基于swfif的ios也是非常方便的一件事情。于是我最终下定决心，定下来的就是打造一个iOS应用作为我的Final Project!😃

## 初期的准备工作
0. 为了打造一款iOS的app，我们肯定需要一些较为简单的教程，但是CS50并没有涉及到如何打造一款iOS的app，因此，我们需要一些在网上找一些教程。我在google搜索"how to build an ios app"![emoji_card_game_0](/assets/images/cs50/cs50_final_project_emoji_card_game_1.png)
我选择了选择了iOS Academy制作的[非常简单的教程iOS](https://www.youtube.com/watch?v=nqTcAzPS3oc)，大概只需要二十分钟
1. 这个视频会教你如何制作一个非常简单的app，就是先通过swfit的selector来选择一些表情，当用户点击了下面的小表情之后之后就可以看到一个大号版的表情在上面。
2. 接着我在借助gpt以及网上关于swifit的教程，开始对这个原始版本的软件进行修改

## Improvement
* 为了更好的改进，我想到每次内部都会进行一个随机的答案。
* 每个表情就是一个随机的选项，就像做选择题一样ABCD随机选择，只有一个表情是正确的。并且会统计用户每次做题的记录
* 点击check是提交答案
* 点击refresh是复原，并且重新随机生一个新的答案

