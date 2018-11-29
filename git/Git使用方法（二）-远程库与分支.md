---
title: Git使用方法（二）-远程库与分支
tags: 
notebook: Elegent
---
# Git使用方法（二）-远程库与分支
本文参考博客[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)整理而成

## 远程库
### SSH Key
1. 创建`SSH Key`: `$ ssh-keygen -t rsa -C "youremail@example.com"`
2. 添加我的`id_rsa.pub`内容至我的远程 git 服务器账户。
### 本地库关联远程库/推送至远程库
1. 关联一个远程库，在本地仓库下使用命令`git remote add origin git@server-name:path/repo-name.git`；
2. 关联后，使用命令`git push -u origin master`第一次推送`master`分支的所有内容；
3. 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改
4. 推送分支到远程库：`git push origin <local-branch-name>:<remote-branch-name>`
    推送本地的`<local-branch-name>`分支到远程origin的`<remote-branch-name>`分支(没有会自动创建)

### 从远程库克隆
1. 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。
    - `$ git clone git@server-name:path/repo-name.git`
2. Git支持多种协议，包括`https`，但通过`ssh`支持的原生`git`协议速度最快。

## 分支管理
### 创建与合并分支
- 查看分支：`git branch`

- 创建分支：`git branch <name>`

- 切换分支：`git checkout <name>`

- 创建+切换分支：`git checkout -b <name>`

- 合并某分支到当前分支：`git merge <name>`

- 删除分支：`git branch -d <name>`

### 解决冲突
- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，先add，再提交，合并完成。解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

- 用`git log --graph`命令可以看到分支合并图

    >`git log --graph --pretty=oneline --abbrev-commit`

### 分支管理策略
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式(`--no-ff`方式的`git merge`)，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
> `git merge --no-ff -m "commit_message" branch_name`

>在实际开发中，我们应该按照几个基本原则进行分支管理：
>>首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
>>那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
>>你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

>合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

### Bug分支
stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。
在当前分支不是working tree clean的情况下，不能切换分支。如果需要切换分支，则需要stash功能。
>`git stash`    //储存当前工作现场
>`git stash list` //查看当前的stash
>`git stash apply stash@{0}` //将当前场景恢复到stash时候
>`git stash drop stash@{0}`  //删除stash
>`git stash pop`  //恢复的同时把stash内容也删了
>>**NOTICE**：如果在当前分支使用`git stash apply`命令恢复其他分支的stash，**git会自动merge当前分支和stash的内容**。

### feature分支
添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。
>在分支没有 merge的情况下，`git branch -d <name>`删除分支操作将无法进行，如果需要强行删除，需要使用`git branch -D <name>`。

### 多人协作
- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

>多人协作工作模式：
>1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
>2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
>3. 如果合并有冲突，则解决冲突，并在本地提交；
>4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！
>5. 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to origin/<branch-name> <branch-name>`。