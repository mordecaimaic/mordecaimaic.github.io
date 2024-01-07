---
title: [Spoil攻略] CS 61B Labs and Projects Challenges Journal
author: mordecaimaic
date: 2023-12-06 18:05:00 +0800
categories: [CS自学, CS 61B]
tags: [cs61]     # TAG names should always be lowercase
---

## week 1

### Lab 1: JSetting Up Your Computer IntelliJ Setup
* 安装Intellj IDEA
* 安装Java JDK
* 安装Git
* 同步CS61b Skeleton Spring 2021 Github 仓库
* 注意⚠️Redaing 1.2 里面的视频和Video List的不匹配，一定要对应看Git Book里面的内容。Git BooK和 Youtube Video List的要对应着看！！！！！

### HW 0: HW0: Basic Java Programs (optional)
* 没有学过Java的话，强烈推荐一定要去做

### Project 0 2048
* 不难，跟着教程说明一步步做就可以了

## week 2 
* week 2 主要讲解如何使用Java的debugger，以及如何使用Junit来进行测试

### Lab 2 Debugging
* 在配置Lab 2 之前，要先进入Lab 2 setup 里面，跟着教程做就好了
* 因为`git submodule update --init`，这个命令是将cs61b的library下载到本地，因为cs61 b 的library是一个submodule，它链接到另外一个地方git仓库，所以要用这个命令来下载。
* 如果不用这个命令的话，就会出现`java: package jh61b.junit does not exist`的错误。
* 只要完成了cs61b setup的设置，能够通过导入XML文件来导入cs61b的library，就可以正常运行Lab 2 了。


## week 3
* 这一周主要讲两种方法实现的List，一种是SLList，一种是Array List。前面这两种 Josh 都是手把手带着敲的，还有是还有是(循环)双向链表，但是老师只是上课提到了理念，所以最好自己动手去实现一下。
* 注意⚠️Redaing 4.1 里面的视频和Video List的不匹配，一定要对应看Git Book里面的内容。Git BooK和 Youtube Video List的要对应着看！！！！！


### Lab3: Randomizing Testing and Timing
* 用随机测试来找到错误，非常巧妙

### discussion
* 第三个有点巧妙，但是听了讲解之后，发现为什么要使用reverse()就不难了，因为reverse()可以将链表反转，然后再使用addFirst()，就可以将链表的顺序反转了。

### Project 1
* 要先根据老师的教程，将作业配置好环境，然后再开始做作业。
* 这个project在学完 week 3 之后，只能做一部分，剩下的部分要等到学完 week 4 之后才能做完。
* Deque：是Double Ended Queue的缩写，就是双向队列，可以从两端进行操作的队列，允许两端都进，两端都出。
*  Linked List Deque的实现: 使用链表来实现Deque，这样子就可以在两端进行操作了。两种实现方法，方法一： two sentinel topology（两个哨兵节点，一个在开始，另一个在结束），方法二：circular topology（循环链表，最后一个节点指向第一个节点）。我使用的是方法二，老师也推荐我们使用方法二
