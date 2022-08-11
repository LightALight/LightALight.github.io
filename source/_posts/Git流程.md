---
title: Git流程
date: 2016-01-13 20:12:32
tags: git
copyright: true
password:
toc: true
---

文章介绍Git的项目工作流程。
<!--more-->
## Quick Guide

### 基本流程

####  模块
![](/image/Git流程/Git流程_001.png)
- Workspace：工作区 就是你在电脑里能看到的目录。
- Index / Stage：暂存区 英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- Repository：仓库区（或本地仓库） 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
- Remote：远程仓库 Git服务器的仓库(自己搭建或者托管平台),存储对应项目代码

#### 一般工作流程如下

1. git clone:克隆 Git 资源作为工作目录。
2. 在克隆的资源上添加或修改文件。注意：修改前保证代码的最新，不然提交可能产生冲突需要解决（git pull）
3. git add:提交修改或者新增到暂存库。
4. git diff:在提交前查看修改。错误，可以撤回提交（git reset HEAD）
5. git commit：提交修改到本地仓库。如果错误，可以撤回提交（git reset commit_id 或 git revert）
6. git push:提交修改到远端仓库。

#### 更新代码

1. git fetch origin master 从远程的origin的master主分支下载最新的版本到origin/master分支上   
2. git stash 把当前修改放入暂存库    
3. git log -p master origin/master 比较本地的master分支和origin/master分支的差别    
4. git merge origin/master 合并master代码到当前分支   
5.  git stash pop 把修改从暂存看恢复回来来

### 流程类型

#### 1.集中式工作流

类似`Subversion`，集中式工作流让你无需去适应一个全新流程就可以体验`Git`带来的收益。这个工作流也可以作为向更`Git`风格工作流迁移的友好过渡。

![](/image/Git流程/Git流程_002.png)

##### 常用命令

```bash
# 1.合并上游的修改到自己的仓库
git pull --rebase origin master
# 2.查看冲突文件
git status
# 3.修改完成后，用老套路暂存这些文件，并让git rebase完成剩下的事
git add <some-file> 
git rebase --continue
# 4.修改完推送
git push origin master
# 如果你碰到了冲突，但发现搞不定，不要惊慌。只要执行下面这条命令，就可以回到你执行git pull --rebase命令前的样子
git rebase --abort
```

####  2.功能分支工作流

功能分支工作流以集中式工作流为基础，不同的是为各个新功能分配一个专门的分支来开发。这样可以在把新功能集成到正式项目前，用`Pull Requests`的方式讨论变更。

![](/image/Git流程/Git流程_003.png)

##### 常用命令

```bash
# 1.在开始开发功能前，使用下面的命令新建一个分支：
git checkout -b marys-feature master
# 2.这个新分支上，小红按老套路编辑、暂存和提交修改，按需要提交以实现功能
git status
git add <some-file>
git commit
git push -u origin marys-feature
```

#### 3.Gitflow工作流

`Gitflow`工作流通过为功能开发、发布准备和维护分配独立的分支，让发布迭代过程更流畅。严格的分支模型也为大型项目提供了一些非常必要的结构。

![](/image/Git流程/Git流程_004.png)

##### 常用命令

```bash
# 1.创建开发分支
git branch develop
git push -u origin develop

# 2.基于develop分支产生功能分支
git checkout -b some-feature develop

# 3.老套路添加提交到各自功能分支上：编辑、暂存、提交：
git status
git add <some-file>
git commit
# 4.功能开发完合并到开发分支
git pull origin develop
git checkout develop
git merge some-feature
git push
git branch -d some-feature
# 5.准备发布
git checkout -b release-0.1 develop
# 6.完成发布，合并修改到master分支和develop分支上，删除发布分支
git checkout master
git merge release-0.1
git push
git checkout develop
git merge release-0.1
git push
git branch -d release-0.1
# 7.发布分支是作为功能开发（develop分支）和对外发布（master分支）间的缓冲。只要有合并到master分支，就应该打好Tag以方便跟踪。
git tag -a 0.1 -m "Initial public release" master
git push --tags

# 1.线上发现bug，从master分支上拉出了一个维护分支，提交修改以解决问题，然后直接合并回master分支
git checkout -b issue-#001 master
# Fix the bug
git checkout master
git merge issue-#001
git push
# 2.新加这些重要修改需要包含到develop分支，并删除维护分支
git checkout develop
git merge issue-#001
git push
git branch -d issue-#001
```

#### 4.Forking工作流

`Forking`工作流是分布式工作流，充分利用了`Git`在分支和克隆上的优势。可以安全可靠地管理大团队的开发者（`developer`），并能接受不信任贡献者（`contributor`）的提交。

![](/image/Git流程/Git流程_005.png)

##### 常用命令：

```bash
# 1.项目维护者初始化正式仓库
git init --bare /path/to/repo.git
# 2.开发者fork正式仓库
git clone https://user@bitbucket.org/user/repo.git
# 3.orking工作流需要2个远程别名 —— 一个指向正式仓库，另一个指向开发者自己的服务端仓库。别名的名字可以任意命名，常见的约定是使用origin作为远程克隆的仓库的别名 （这个别名会在运行git clone自动创建），upstream（上游）作为正式仓库的别名。
git remote add upstream https://bitbucket.org/maintainer/repo
# 4.开发者开发自己的功能
git checkout -b some-feature
# Edit some code
git commit -a -m "Add first draft of some feature"
# 5.用git pull命令获得新的提交
git pull upstream master
# 6.开发者发布自己的功能
git push origin feature-branch
# 7.使用Pull Request提交到正式仓库
# 8.维护者需要从开发者的服务端仓库中fetch功能分支， 合并到他本地的master分支
git fetch https://bitbucket.org/user/repo feature-branch
# 查看变更
git checkout master
git merge FETCH_HEAD
# 9.开发者和正式仓库做同步
git push origin master
```

####  5.Pull Requests

`Pull requests`是`Bitbucket`提供的让开发者更方便地进行协作的功能，提供了友好的`Web`界面可以在提议的修改合并到正式项目之前对修改进行讨论。

开发者向团队成员通知功能开发已经完成，`Pull Requests`是最简单的用法。 开发者完成功能开发后，通过`Bitbucket`账号发起一个`Pull Request`。 这样让涉及这个功能的所有人知道要去做`Code Review`和合并到`master`分支。

- 在功能分支工作流中使用Pull Request

![](/image/Git流程/Git流程_006.png)

- 在Gitflow工作流中使用Pull Request

![](/image/Git流程/Git流程_007.png)

- 在Forking工作流中使用Pull Request

![](/image/Git流程/Git流程_008.png)

###  企业日常开发模式探索

解决的需求场景如下：

- 能支持日常迭代开发、紧急线上bug修复、多功能并行开发
- 大概50人左右的团队，平日迭代项目较多，且周期短（1~2周一个迭代）
- 能够通过tag重建整个系统
- 支持code review
- 所有上线的代码必须都是经过测试保证，且能自动同步到下一次的迭代中
- 能和公司的项目管理/持续集成系统整合

![](/image/Git流程/Git流程_009.png)

1. 迭代需求会、冲刺会后确定本次迭代的目标后，将迭代内容视为一个项目，在 Gitlab 上创建一个 Repository，初始化工程代码结构，根据上线日期，比如20150730上线，开出分支 release20150730、dev20150730 两个分支，dev 分支作为日常开发主干分支，release 分支作为提测打包、Code Review 的分支。
2. 迭代开始，日常开发进行中，开发人员在 dev 分支上进行 Commit、Push 代码，并且解决掉日常协同开发中的冲突等问题，等到达到提测条件的时候，提测者，首先 Merge Master 分支上的最新代码 `git merge --no-ff origin/master` ，使得 Master 分支上的变更更新到迭代开发分支dev上面，之后，在 Gitlab 上面发起 `pull request` 请求，并指定 Code Review 人，请求的分支选择本次上线的 release 分支，即 release20150730。
3. 被指定 Code Review 的人，对发起者的代码 Review 后，决定是否可以提交测试，若有问题，评论注释代码后，提交者对代码进行进行修改，重复步骤2，直到代码 Review 者认为 Ok。之后便可以借助自己公司的打包部署，对这些代码发布到测试环境验证。
4. 步骤2-3重复多次后，就会达到一个稳定可发布的版本，即上线版本，上线后，将 release 版本上面最后的提交（图中0.2.4上线对应处）合并到 Master 分支上面，并打 Tag0.3。至此，一次完整的迭代开发完成。
5. 若此次上线后，不久发现生产环境有 Bug 需要修复，则从 Tag 处新开分支 release_bugfix_20150731、dev_bugfix_20150731 ，开发人员从 dev_bugfix_20150731分支上进行开发，提测code review在 release_bugfix_20150731 分支上，具体步骤参考2-3，测试环境验证通过后，发布到线上，验证OK，合并到 Master 分支，并打 Tag0.2.3，此次 Bug 修复完毕，专为解 Bug 而生的这两个分支可以退伍了，删除release_bugfix_20150731、dev_bugfix_20150731两分支即可。（所有的历史 Commit 信息均已经提交到了 Master 分支上，不用担心丢失）

![](/image/Git流程/Git流程_010.png)

- master：master永远是线上代码，最稳定的分支，存放的是随时可供在生产环境中部署的代码，当开发活动告一段落，产生了一份新的可供部署的代码时，发布成功之后，代码才会由 aone2 提交到 master，master 分支上的代码会被更新。应用上 aone2 后禁掉所有人的 master的写权限
- develop：保存当前最新开发成果的分支。通常这个分支上的代码也是可进行每日夜间发布的代码，只对开发负责人开放develop权限。
- feature: 功能特性分支，每个功能特性一个 feature/ 分支，开发完成自测通过后合并入 develop 分支。可以从 master 或者develop 中拉出来。
- hotfix: 紧急bug分支修复分支。修复上线后，可以直接合并入master。

![](/image/Git流程/Git流程_011.png)

- master：master永远是线上代码，最稳定的分支，存放的是随时可供在生产环境中部署的代码，当开发活动告一段落，产生了一份新的可供部署的代码时，发布成功之后，代码才会由 aone2 提交到 master，master 分支上的代码会被更新。应用上 aone2 后禁掉所有人的 master的写权限
- develop：保存当前最新开发成果的分支。通常这个分支上的代码也是可进行每日夜间发布的代码，只对开发负责人开放develop权限。
- feature: 功能特性分支，每个功能特性一个 feature/ 分支，开发完成自测通过后合并入 develop 分支。可以从 master 或者develop 中拉出来。
- hotfix: 紧急bug分支修复分支。修复上线后，可以直接合并入master。