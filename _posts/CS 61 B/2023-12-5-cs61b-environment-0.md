---
title: CS 61B Junit 环境配置踩坑记录
author: mordecaimaic
date: 2023-12-05 19:50:00 +0800
categories: [CS自学, CS 61B]
tags: [cs61]     # TAG names should always be lowercase
---
在做cs61b 2.5的alist的lecture exercise的时候，发现有一个语句使用了`jh61b.junit.TestRunner.runTests("all", AListTest.class);`

但是编译器提示找不到jh61b.junit

经过一番查找折腾之后，才发现我之前使用的软件测试junit是Intellij自己帮我们下载好的

而cs61b使用的是在cs61b里面老师写好的library，里面有jh61b.junit(我猜应该是Josh Hug 61B的意思，老师的名字)

所以我们一定要使用cs61b的skeleton的libray！！！

如何使用cs61b的library呢？如果已经完成project 0的话，里面的教程就会有讲到

1. 完成cs61b的library的配置,在Intellij里面，点击`File`->`Project Structure`->`Libraries`->`+`->`Java`->选择`cs61b`文件夹里面的`library`文件夹
   
   ![cs61b library配置](/assets/images/cs61b/intellij-setup.gif)

2. 点击`File`->`Project Structure`->`Modules`->`Dependencies`，如果已经配置了Junitd的话，要先把Junit的依赖删掉，按上面的`-`。
然后再点击->`+`->选择`cs61b`文件夹里面的->`library-sp21`->`javalib`文件夹。，然后再添加cs61b的依赖。

   ![cs61b library配置](/assets/images/cs61b/cs61b_module_configure.png)

3. 然后cs61b aLitst的test程序就可以正常运作了。