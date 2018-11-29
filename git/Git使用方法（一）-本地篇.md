---
title: Git 使用方法（一）-本地篇
tags: 
notebook: Elegent
---
# Git 使用方法（一）-本地篇
本文参考博客[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)整理而成

## 自报家门，设置本机信息
```git
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
>- 注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的`Git`仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和`Email`地址。
>- 自己的不同机器可以用同样的`user.name`和`user.email`。不同机器产生的`SSH Key`是不同的。
## 初始化Git仓库
>`git init`

添加文件到Git仓库，分两步：

>1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
>2. 使用命令`git commit -m <message>`，完成。
>3. `git add .` 将当前git目录下的所有改变提交到暂存区

## 查看工作区的状态和改变
>- 要随时掌握工作区的状态，使用`git status`命令。
>- 如果git status告诉你有文件被修改过，用`git diff`可以查看修改内容。
>- `git diff`终端变成查看模式，不能打命令了，此时按两下`Esc`然后按`q`即可输入命令。
![不同的git diff](http://yaozhuwa-bucket.oss-cn-beijing.aliyuncs.com/18-11-7/25057352.jpg)

## 版本穿梭
>- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
>- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。
>- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
>    - 在Git中，用`HEAD`表示当前版本，也就是最新的提交`1094adb...`（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版
本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。

## 版本库（Repository）
>- 工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。
>- Git的版本库里存了很多东西，其中最重要的就是称为`stage`（或者叫`index`）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

## 管理修改
>- 提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别
>- 提交的是`add`到暂存区`stage`的部分，没有`add`的部分修改不会被`commit`到最新版本。

### 撤销修改
>`git checkout -- <file>`
>命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：
>>- 一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
>>- 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
>>>总之，就是让这个文件**回到最近一次git commit或git add时的状态**。

>`git reset HEAD <file>`可以把暂存区的修改撤销掉（`unstage`），重新放回工作区

>小结：
>- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- <file>`。
>- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。
>- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 删除文件
>`rm <file>`删除文件，或者直接在资源管理器删除文件
>1. 确实要从版本库中删除该文件，那就用命令`git rm <file>`删掉，并且`git commit`:
`git rm test.txt`
`git commit -m "remove test.txt"`
>2. 删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本:
`git checkout -- test.txt`
>3. `git rm`删除文件，那就相当于不仅删除了文件，而且还添加到了暂存区，如果想要恢复:
`git reset HEAD <file>`
`git checkout -- <file>`


