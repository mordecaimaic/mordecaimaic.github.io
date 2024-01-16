---
title: CS 61B Week 4 Discussion "Dynamaic Method Selection"
author: mordecaimaic
date: 2024-01-16 10:30:00 +0800
categories: [CS自学, CS 61B]
tags: [cs61]     # TAG names should always be lowercase
---

## 问题解析
这是week4 - Discussion: "Inheritance and Implements Exam Prep"里面的第二题。
这道题目非常巧妙，结合了extend+递归的用法让我们来看看原题。

> Dynamic Method Selection
Modify the code below so that the max method of DMSList works properly. Assume all numbers inserted into DMSList are positive, and we only insert using
insertFront. You may not change anything in the given code. You may only fill
in blanks. You may not need all blanks. (Spring ’16, MT1)
    
```java
1 public class DMSList {
2 private IntNode sentinel;
3 public DMSList() {
4 sentinel = new IntNode(-1000, _____________________);
5 }
6 public class IntNode {
7 public int item;
8 public IntNode next;
9 public IntNode(int i, IntNode h) {
10 item = i;
11 next = h;
12 }
13 public int max() {
14 return Math.max(item, next.max());
15 }
16 }
17 public _________________________________ {
18
19 ____________________________________________________________
20
21 ____________________________________________________________
22
23 ____________________________________________________________
24
25 ____________________________________________________________
26
27 ____________________________________________________________
28
29 ____________________________________________________________
30
31 ____________________________________________________________
32
33 ____________________________________________________________
34 }
35 /* Returns 0 if list is empty. Otherwise, returns the max element. */
36 public int max() {
37 return sentinel.next.max();
38 }
39 public void insertFront(int x) { sentinel.next = new IntNode(x, sentinel.next); }
40 }
```
总结一下题目的要求
* 要求我们在调用`max()`的函数，能够List里面的最大值，并且如果List为空的话，返回0
* 首先我们来解读一下`max()`函数，当调用`max()`的时候，会返回第37行的`sentinel.next.max()`。由于`sentinel.next`是一个IntNode类型的对象，所以会调用IntNode的`max()`函数。
* 然后我们会进入到第13行的函数，将会返回第14行的`Math.max(item, next.max())`。由于我们在外面是使用`sentinel.next.max()`来调用的，所以`item`指的是`sentinel.next.item`，`next`指的是`sentinel.next.next`。
* 假设我们有一个List是`sentinel->1->2`，这时候我们调用`max()`函数。我们分别将`1`所在的结点记为`node1`，将`2`所在的结点记为`node2`。那么`sentinel.next`将会是`node1`结点。
* 进入到第`14`行里面，我们将会调用`Math.max(1, node2.max())`。
* 在调用`node2.max()`的时候，我们会进入到第13行的函数，将会返回第14行的`Math.max(2, node2.next.max())`。但是由于`ndoe2.next`是`null`，我们在下一次进行调用的时候，将会出现`NullPointerException`的错误。
* **这说明我们需要设置一个base case**，也就是设置一个特殊的节点，该节点始终在List最尾端。该节点的`max()`也是特殊的，它将会直接返回`0`。
* 并且在第`4`行的时候，当我们创建一个新的`DMSList`的时候，我们需要将`sentinel.next`指向这个节点。
* 这样子我们在List为空的时候，我们的List将会是`sentinel->LastIntNode`，这样子，我们在调用LastIntNode里面的特殊的`max()`，将会直接返回`0`。

## solution
以下是solution的代码，我在代码里面加了一些注释，帮助大家理解。
```java
Solution:
1 public class DMSList {
2 private IntNode sentinel;
3 public DMSList() {
4 sentinel = new IntNode(-1000, new LastIntNode()); // 让sentinel指向一个新的IntNode，这个IntNode的item是-1000，next是一个LastIntNode。
5 }
6 public class IntNode {
7 public int item;
8 public IntNode next;
9 public IntNode(int i, IntNode h) {
10 item = i;
11 next = h;
12 }
13 public int max() {
14 return Math.max(item, next.max());
15 }
16 }
17 public class LastIntNode extends IntNode {// 创建一个LastIntNode，让它继承IntNode
18 public LastIntNode() {
19 super(0, null); //调用父类的构造函数，让它的item是0，next是null
20 }
21 @Override
22 public int max() {
23 return 0;//override父类的max()，让它返回0。(相当于是basecase)
24 }
25 }
26 /* Returns 0 if list is empty. Otherwise, returns the max element. */
27 public int max() {
28 return sentinel.next.max();
29 }
30 public void insertFront(int x) {
31 sentinel.next = new IntNode(x, sentinel.next);
32 }
33 }
```