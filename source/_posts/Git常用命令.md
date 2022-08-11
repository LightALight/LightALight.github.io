---
title: Git常用命令
date: 2015-12-13 20:12:32
tags: git
copyright: true
password:
toc: true
---

Git是一个开源的分布式版本控制系统，用于敏捷高效地处理项目。文章介绍Git的常用命令。
<!--more-->
## Quick Guide

### 基本命令
* 1.工作区域

    ![](/image/Git常用命令_001.jpg)
    - 工作区(workspace)：就是你在电脑里能看到的目录。
    - 暂存区(Index/Stage)：英文叫stage, 或index。一般存放在 ".git目录下" 下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
    - 版本库(master):工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
    - 远端仓库(Remote): Git服务器的仓库(自己搭建或者托管平台),存储对应项目代码

* 2.文件的状态
    - 未修改(Origin)
    - 已修改(Modified)
    - 已暂存(Staged)
    - 已提交(Committed)
    - 已推送(Pushed)

* 3.基本操作

    - git add:把工作区的文件放入暂存区

        ```bash
        git add <path> # 把工作区的文件修改提交到暂存区
        git add . # 提交工作区的所有文件修改
        ```

    - git commit：把文件从暂存区提交进本地仓库

        ```bash
        git commit -m "the commit message" # 提交当前暂存区的修改记录
        git commit -a # 会先把所有已经track的文件的改动`git add`进来，然后提交。
        git commit --amend # 增补提交，会使用与当前提交节点相同的父节点进行一次新的提交，旧的提交将会被取消。
        ```

    - git push:把文件从本地仓库推送进远程仓库

        ```bash
        git push <远程主机名> <本地分支名>:<远程分支名> # 从 Git 本地仓库中更新到远端仓库
        git push origin [tagname] # 分享标签
        ```

* 4.检查修改以及回滚

    - git diff:在提交前工作目录中当前文件和暂存区域快照之间的差异,。如果错误，可以撤回提交（git reset HEAD）

        ```bash
        git diff <file> # 比较当前文件和暂存区文件差异
        git diff <id1><id1><id2> # 比较两次提交之间的差异
        git diff <branch1> <branch2> # 在两个分支之间比较
        git diff # 比较未修改和已修改后差异---已修改，未暂存
        git diff --staged # 比较暂存区和版本库差异---已未暂存，未提交
        git diff --cached # 比较暂存区和版本库差异---已未暂存，未提交
        git diff <当前分支> <远程主机名/远端分支> # 比较本地分支和远端分支的差异---已提交，未推送
        git diff --stat # 仅仅比较统计信息
        ```

    - git reset:将HEAD指向的位置改变为之前存在的某个版本,用于撤消之前的一些操作(add, commit)

        ```bash
        git reset --hard # 回退到上个版本，放弃版本后的修改、暂存和提交
        git reset --mixed # mixed是默认参数，回退到上个版本，放弃版本后的暂存和提交
        git reset --soft # 回退到上个版本，放弃版本后的提交
        git reset --hard HEAD~n # 回退n个版本
        git reset --hard <commit_id> # 回滚到指定版本，修改不能保存
        ```
    - git revert:同reset，只不过撤销操作之前和之后的commit和history都会保留，并且把这次撤销作为一次最新的提交

        ```bash
        git revert HEAD # 撤销前一次 commit
        git revert HEAD^ # 撤销前前一次 commit
        git revert <commit-id> # 撤回指定commit-id
        ```

* 5.其他基本命令

    - git init：初始化一个 Git 仓库

        ```bash
        git init newrepo # 指定目录作为Git仓库
        ```

    - git config：命令用于获取并设置存储库或全局选项

        ```bash
        git config --global user.name "xiaoming" # 设置全局用户名
        git config --global user.email "xiaoming@gmail.com" # 设置全局邮箱
        git config --global core.editor emacs # 设置编缉器
        git config --global merge.tool vimdiff # 设置比较工具，比较工具用来解决合并时的冲突
        git config --list # 检查配置
        ```

    - git clone:克隆 Git 资源作为工作目录。

        ```bash
        git clone <repo> <directory> # 从现有 Git 仓库中拷贝项目克隆到指定的目录
        ```

    - git pull:是从远程获取最新版本到本地，并自动merge

        ```bash
        git pull <远程主机名> <远程分支名>:<本地分支名> # 从 Git 远端仓库中更新到本地仓库
        ```

    - git status:显示文件修改是否被暂存或者tracked。

        ```bash
        git status
        ```

    - git branch：用于列出，创建或删除分支。

        ```bash
        git branch # 查看当前有哪些分支
        git branch <分支> # 新建分支
        git branch -d <分支> # 删除分支
        ```

    - git checkout:用于切换分支或恢复工作树文件。

        ```bash
        git checkout <文件> # 还原文件的修改
        git checkout <分支> # 切换分支
        git checkout -b <分支> # 创建并切换分支
        ```

    - git log:用于显示提交日志信息

        ```bash
        git log [<options>] [<revision range>] [[\--] <path>…]
        ```

    - git stash:用于将改过的被追踪的文件和暂存的变更储藏在脏工作目录中（refs/stas）

        ```bash
        git stash # 将当前的修改和暂存储藏存储起来，用于更新远端分支产生冲突时候
        git stash list # 查看储藏
        git stash pop # 释放储藏
        ```

    - git fetch:命令用于从另一个存储库下载对象和引用。

        ```bash
        git fetch origin # 从远程refs/heads/命名空间复制所有分支，并将它们存储到本地的refs/remotes/origin/命名空间中
        git fetch <远程主机名> <分支名> # 更新远程主机的分支到本地
        ```

    - git merge:用于将两个或两个以上的开发历史加入(合并)一起

        ```bash
        git merge <分支>1… <分支2>… # 合并分支到当前分支
        git merge <远程主机名/分支名> # 合并fetch的分支到当前分支
        ```

    - git rebase:用于把一个分支的修改合并到当前分支,放弃一个分支的记录

        ```bash
        git rebase <分支>1… <分支2>… # 合并分支到当前分支
        git rebase <远程主机名/分支名> # 合并fetch的分支到当前分支
        ```

    - git remote:管理一组跟踪的存储库

        ```bash
        git remote -v # 列出已经存在的远程分支的详细信息
        git remote add <shortname> <url> # 添加远程仓库
        ```

    - git help:显示有关Git的帮助信息。

        ```bash
        git help <verb> # 显示命令的帮助信息
        git <verb> --help # 显示命令的帮助信息
        ```


### 其他

* git rm：用于从工作区和索引中删除文件

    ```bash
    git rm [-f | --force] [-n] [-r] [--cached] [--ignore-unmatch] [--quiet] [--] <file>…
    ```

* git mv：用于移动或重命名文件，目录或符号链接

    ```bash
    git mv <options>… <args>…
    ```

* git mergetool:用于运行合并冲突解决工具来解决合并冲突

    ```bash
    git mergetool [--tool=<tool>] [-y | --[no-]prompt] [<file>…]
    ```

* git tag：用于创建，列出，删除或验证使用GPG签名的标签对象。

    ```bash
    git tag # 列显已有的标签
    git tag -a <tag-name>-m 'version info' # 创建标签
    git tag -s <tag-name>-m 'version info' # 签署标签
    git tag -d # 删除标签
    git tag <tag-name> # 创建轻量级标签
    git tag -v <tag-name> # 验证标签
    git tag -a <tag-name> <command-id> # 后期加注标签
    ```

* git submodule:用于初始化，更新或检查子模块(另外一个仓库)

    ```bash
    git submodule add <url> # 添加子模块
    git submodule init # 初始化本地配置文件的子模块
    git submodule update # 更新子模块
    ```

* git show:用于显示各种类型的对象

    ```bash
    git show [options] <object>…​ # 显示一个或多个对象(blobs，树，标签和提交)
    ```

* git shortlog:用于汇总git日志输出

    ```bash
    git shortlog # 返回这个 git repository 底下每个用户进行 commit 的次数，以及每次 commit 的注释
    ```

* git describe:显示离当前提交最近的标签。

    ```bash
    git describe [--all] [--tags] [--contains] [--abbrev=<n>] [<commit-ish>…​]
    ```


More info: [Git 完整命令手册](https://git-scm.com/docs)
