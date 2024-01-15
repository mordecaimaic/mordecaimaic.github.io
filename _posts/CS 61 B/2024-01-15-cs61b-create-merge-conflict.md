---
title: CS 61B 如何手动创建一个conflict
author: mordecaimaic
date: 2024-01-15 13:35:00 +0800
categories: [CS自学, CS 61B]
tags: [cs61]     # TAG names should always be lowercase
---
> 
在进行cs61 b的lab 4的时候，由于我们不是跟着老师同步学习的，所以我们必须手动创建一个有冲突的文件，然后解决冲突，才能够了解到lab 4的内容。
{: .prompt-tip}
## 如何手动创建一个conflict

创建合并冲突（merge conflict）可以通过以下步骤手动完成。在一个版本控制系统（如Git）中，合并冲突通常发生在两个分支修改了同一文件的相同部分时。下面是一个简单的步骤来手动创建合并冲突：

假设有两个分支，分别是 `branchA` 和 `branchB`。

1. **切换到到`lab1`：**
   ```bash
   cd lab1
   ```

2. **在两个不同的分支上创建并切换：**
   ```bash
   # 创建并切换到 branchA
   git checkout -b branchA

   # 在 branchA 分支上修改文件
   echo "This is branchA content." >> Collatz.java

   # 提交修改
   git add Collatz.java
   git commit -m "Commit on branchA"

   # 切换回主分支
   git checkout master

   # 创建并切换到 branchB
   git checkout -b branchB

   # 在 branchB 分支上修改相同文件的相同位置
   echo "This is branchB content." >> Collatz.java

   # 提交修改
   git add Collatz.java
   git commit -m "Commit on branchB"
   ```

3. **尝试合并两个分支：**
   ```bash
   git checkout master
   git merge branchA
   ```

   这时，你会得到合并冲突的提示。

4. **手动创建冲突：**
   打开文件 `Collatz.java`，你最后面会看到类似如下的内容：
   ```plaintext
   <<<<<<< HEAD
   This is branchB content.
   =======
   This is branchA content.
   >>>>>>> branchA
   ```

   上面的部分是 `HEAD`（当前分支，即 `master` 分支）的内容，中间的 `=======` 表示冲突的分割线，下面的部分是 `branchA` 分支的内容。

5. **手动解决冲突：**
   你需要手动选择保留哪个分支的内容或者做其他修改。删除或修改冲突标记（`<<<<<<<`、`=======`、`>>>>>>>`）并留下你想要的结果。

6. **标记冲突已解决：**
   保存文件后，使用以下命令告诉Git你已经解决了冲突：
   ```bash
   git add Collatz.java
   ```

7. **完成合并：**
   ```bash
   git merge --continue
   ```

现在，你手动创建了一个合并冲突，并且解决了这个冲突。
