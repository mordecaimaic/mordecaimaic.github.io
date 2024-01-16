---
title: CS 61B 攻略
author: mordecaimaic
date: 2023-12-06 18:05:00 +0800
categories: [CS自学, CS 61B]
tags: [cs61]     # TAG names should always be lowercase
---

***

## week 1

### Lab 1: JSetting Up Your Computer IntelliJ Setup
* 安装Intellj IDEA
* 安装Java JDK
* 安装Git
* 同步CS61b Skeleton Spring 2021 Github 仓库，在google上就能够找到对应的地址。[老师的代码框架](https://github.com/mordecaimaic/skeleton-sp21)
* 注意⚠️Redaing 1.2 里面的视频和Video List的不匹配，一定要对应看Git Book里面的内容。Git BooK和 Youtube Video List的要对应着看！！！
* 如果对Git或者Git较为熟悉的同学，配置这里应该也不难。

***

### HW 0: HW0: Basic Java Programs (optional)
* 涉及到一些Java最基本的概念以及方法，没有学过Java的话，强烈推荐一定要去做

***

### Project 0 2048
* 不难，复刻一个2048的游戏。主要是操作一些二维数组就可以了，跟着教程说明一步步做就可以了。

***

## week 2 
* week 2 主要讲解如何使用Java的debugger，以及如何使用Junit来进行测试

***

### Lab 2 Debugging
* 这个Lab 2 的实验我整整配置了半天时间才弄好，下面是我我踩过的一些坑。
* 在配置Lab 2 之前，根据提示，先进入Lab 2 setup 里面，跟着教程一步步做。
* 因为`git submodule update --init`，这个命令是将cs61b的library下载到本地，因为cs61 b 的library是一个submodule，它链接到另外一个地方git仓库，所以要用这个命令来下载。
* 如果命令无法下载submodule的话，我们可以直接去到submodule的链接里面下载，然后放到本地的cs61b的library里面。
* 如果不用这个命令的话，就会出现`java: package jh61b.junit does not exist`的错误。
* 只要完成了cs61b setup的设置，能够通过导入XML文件来导入cs61b的library，就可以正常运行Lab 2 了。
* 下图为代码仓库中的submodule：
* ![cs61b submodule](/assets/images/cs61b/cs61b_submodule.png)
* 在cs61b skeleton中会有这种标志的文件夹，在使用git clone的时候是不会下载的，这个是我们链接到别处仓库的。所以要使用`git submodule update --init`来下载。或者是手动下载，然后放到对应的文件夹里面。

***

## week 3
* 这一周主要讲两种方法实现的List，一种是SLList，一种是Array List。前面这两种 Josh 都是手把手带着敲的，还有是还有是(循环)双向链表，但是老师只是上课提到了理念，所以最好自己动手去实现一下。
* 注意⚠️Redaing 4.1 里面的视频和Video List的不匹配，一定要对应看Git Book里面的内容。Git BooK和 Youtube Video List的要对应着看！！！！！

***

### Lab3: Randomizing Testing and Timing
* 用随机测试来找到错误，非常巧妙，我们可以随机生成的数字，做一些随机的动作，然后进行测试，看看是否会出现错误。

***
### discussion: Linked Lists Exam Prep
* 第三个有点巧妙，但是听了讲解之后，发现为什么要使用reverse()就不难了，因为reverse()可以将链表反转，然后再使用addFirst()，就可以将链表的顺序反转了。

***

### Project 1
* 要先根据老师的教程，将作业配置好环境，然后再开始做作业。只要耐心阅读教程即可，保证将任务分解成一点点进行解决即可。
* 这个project在学完 week 3 之后，只能做一部分，剩下的部分要等到学完 week 4 之后才能做完。
* 这个project主要围绕的是Deque：是Double Ended Queue的缩写，就是双向队列，可以从两端进行操作的队列，允许两端都进，两端都出。
####  Linked List Deque的实现: 
* 使用链表来实现Deque，这样子就可以在两端进行操作了。两种实现方法，**方法一： two sentinel topology（两个哨兵节点，一个在开始，另一个在结束）**
* **方法二：circular topology（循环链表，最后一个节点指向第一个节点）。我使用的是方法二，老师也推荐我们使用方法二**
####  Array Deque的实现: 
* 我第一次做，比较烧脑没想出来。project使用数组来实现Deque,要用一个front和一个rear来指向数组的头和尾，模拟双向循环链表的操作。但是由于我想了很久，都没有想到要怎么做，所以我在google上搜索了how to use array to implement Deque，找到了这篇文章：[Implementation of Deque using circular array- GeeksforGeeks](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)，里面有原理+伪代码+图片的解释，我的ArrayDedue的addFirst()以及addLast()具体就是根据这篇文章来实现的。
* 关于数组的调整部分，下面是难点：
* 老师也在project里面说到了，这个部分是"Very Tricky"的，关于这个问题，我也是思考了很久后，通过Debug，自己解决出来了，**其实最重要的就是System.arraycopy()的参数的设置，关于这部分内容，只要先看懂了我上面贴的博客，然后再自己思考一下就可以了，不难但巧妙**。
* 需要注意的是我们要根据已经存放的元素的个数，和已经创建的数组的长度来判断是否需要扩容或者缩容。如果数组满了的话，我们要进行doubleSize(),也就是将数组进行双倍扩张。
* 如果已经存放的个数，小于数组的长度的0.25倍的话，我们要进行halfSize(),也就是将数组进行缩小一半。
* 最难的是，我们怎么利用System.arraycopy来实现数组的复制。关于这个问题，需要利用到之前设置好的front, rear, 所存放的元素个数，以及数组的长度。具体的思考过程，需要分两种情况讨论，情况1是线性表跨越过数组的边界，情况2是线性表没有跨越过数组的边界。只要将这两种情况想好，借助画图的办法，就可以很容易的想到怎么利用System.arraycopy来实现数组的复制，来进行数组的扩容和缩容。
* 我所利用的办法，是将数组的旧的线性表的front节点，复制到新的数组newArray的最左边的地方。也就是将线性表最左边的元素，复制到newArray[0]。
* **还有一点就是多用Debuger+Java Visualizer!超好用🤠**这两个工具，可以帮助我们很好的理解代码的运行过程，以及变量的变化过程。下面是我在做ArrayDeque的时候，用Java Visualizer来帮助我理解代码的运行过程的图片。
![Debuger + Java Visualizer](/assets/images/cs61b/cs61b_arrayDeque_visualizer.png "Debuger + Java Visualizer")


> 当完成了上面的部分的时候，我们可以去gradescope的project 1 checkpoint里面，先提交作业，看看是不是满分，如果是满分的话，就可以继续做下面的部分了。值得注意的是project 1 checkpoint里面没有对ArrayDeque的resize()进行测试，但是在最终测试的时候，会对resize()进行测试。
{: .prompt-tip }

#### GuitarString的实现
* 这个部分比较简单，虽然作业的文档写的很复杂，写了很多声音的物理原理，看起来很吓人，但是我们只需要根据文档里面的公式，和作业的skeleton里面的老师写的注释来实现GuitarString的类即可，非常简单。
* >（关于声音合成原理，如果这部分内容感兴趣，可以上网查找或者是用chatgpt帮忙解读。我也是跳过了这部分内容😥）
* 如果做完的话，可以用实现的GuitarPlay来玩一下吉他，非常有趣。在GuitarPlay里面按下"q"和"c"应该会听到声音。
* 接下来运行"TTFAF"，正常来说，应该会播放一首完整的用吉他演唱的歌。**注意注意在Guitar里面一定都要用LinkListDeque和ArrayDeque来分别初始化buffer，保证两个Deque都是可以播放一首完整的歌。**
* 因为我在做完的时候，发现我用ArrayDeque初始化GDeque的时候，不能够完成播放一首歌，后来通过Debug发现是我的ArrayDeque的Size调整method有问题。所以一定要保证两个Deque都是可以播放一首完整的歌。
* 接下来，任务已经基本完成了，可以在gradescope上面提交作业了，如果是满分的话，就可以继续做下面的部分了。
* 在完成之后，我们可以看到有一个"Even More Fun"的部分，这个部分我们可以根据不同乐器的发声音原理不同，来实现不同的乐器，比如说钢琴，竖琴，鼓等等，只要按照说明修改算法即可。
#### Autograder(隐藏任务)
* 当完成上面两个之后，我们可以做一个选做任务。这个任务是要求我们利用随机数自己写一个Autograder，来测试老师给我们提供的一个有问题的StudentArrayDeque，并且要求准确地写出错误的序列。
* 这个任务有点巧妙，但是也不难，只要根据老师给的提示，一步步做就可以了。这个额外的作业作业放在了`proj1ec`里面，我当时找了一下才找到。
* **第一步**：找出错误，找出错误很简单。核心思想是：我们利用老师给我们的ArrayDequeSolution也可以利用java自带的LinkedList，同时创建两个循环Deque。我们根据随机数同时对它们做相同的操作，例如add和remove等。我们在每次removeFirst或者removeLast的时候，我们就可以比较两个Deque的remove返回的结果是否相同，**如果发现不相同的话，就说明我们找到了错误。**
**(其实ArrayDequeSolution也是extends了java自带的LinkedList，但是只不过是创建一些异常处理，我使用的是java自带的LinkedList)**
* **第二步**：在找到了错误之后，最关键的是，我们怎么将错误的操作序列输出出来，什么意思呢。我们在发现了错误之后，我们肯定是要知道一个**全新的Deque**在初始化之后是经过了什么操作才会出错的，比如经历了Operation_1, Operation_2, Operation_3...Operation_n，操作了n次之后，通过对比两个Deque我们发现了错误。**我们的关键就是如何将所有的Operation_1, Operation_2, Operation_3...Operation_n全部输出出来，放到asserEquals()里面的报错信息**
* 关于assertEquals的用法，查看一下使用例子就可以了，老师也有Demo展示。

***

## week 4
* 由于projec 1 的iterator以及其他一些内容是在week 4 里面讲解的，因此学学week 4 之后，就能够完成project 1的剩余部分了。

***

### Lab 4: Git and Debugging
* 这个Lab 4可以帮助我们加强git以及debug的能力，这两个能力在以后的学习工作中都是非常重要的。
* 在进入lab 4之前，最好先看一下这个视频[cs50关于git的讲解](https://www.youtube.com/watch?v=MJUJ4wbFm_A&t=454s)。这个视频可以更加概括性的讲解，看完可以有一个入门的理解。
* 这个lab主要讲解了git的基本概念，基本操作。有6个关于git的视频，看完之后理解git的基本概念，基本操作即可，学会怎么merge conflict，怎么使用git来进行版本控制。（例如切换到历史的coommit，将代码文件还原等）
* 注意：由于只有跟着cs61b老师的课程，老师下发一个有冲突版本的代码，让学生能够联系merge conflict，所以我们在做lab 4的时候，没有办法练习merge conflict，但是我们可以在自己的仓库里面，**手动创建一个有冲突的分支，然后练习merge conflict**。

>
关于如何在lab 1里面手动创建一个conflict，然后merge conflict，看我这篇教程，[CS 61B 如何手动创建一个conflict](/posts/cs61b-create-merge-conflict)
{: .prompt-tip }
  * `Lab 4A`和`Lab 4B`的内容，主要解决`lab 1 `里面的`Collatz.java`里面的冲突就可以了。在lab 4A里面，按照老师给的错误代码替换到`Collatz.java`里面的`nextNumber`提交即可。在lab 4b 里面，使用`git log`和`git checkout <commit> -- Collatz.java`来还原代码，然后再提交即可。
* 在`Lab 4: Debugging`里面，主要是解决`lab4/Flik.java`以及测试代码`lab4/HorribleSteve.java`里面错误。这时候我们要用到两个非常重要的debug知识，**conditional breakpoints** 和**breaking on exceptions**，也就是条件断点和异常断点。这两个断点的使用，可以帮助我们更好的debug代码。如果忘记的的话的话，回去复习**Lab 3**的内容即可。
* 利用上面这两种断点，可以找到错误，修复后提交代码，就可以通过lab 4了。
* 按照老师的做法，使用`Junit`也是可以的，具体的做法是：创建一个新的测试文件，使用`assertTrue(boolean)` 和 `assertTrue(String, boolean)`来测试代码。

*** 

### Discussion: Inheritance and Implements Exam Prep
这里有一道题目非常巧妙，我单独开了一篇博客来讲解第2题: ["Dynamic Method Selection"](/)
