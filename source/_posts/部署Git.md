---
title: 部署Git
date: 2015-11-23 20:04:16
tags: git
copyright: true
password:
toc: true
---

这是一个简单的指导说明，介绍如何git部署和配置使用.
<!--more-->

## Quick Start
### 安装

[下载地址](https://git-scm.com/download/gui/windows)

### 配置Git

- 首先在本地创建`ssh key`,后面的`your_email@youremail.com`改为你在github上注册的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。

```bash
ssh-keygen -t rsa -C "your_email@youremail.com"
```

💡 默认在 `.ssh`下面生成两个两个文件 私钥:`id_rsa`  公钥:`id_rsa.pub`


- 在`~/`下生成`.ssh`文件夹，进去，打开`id_rsa.pub`，复制里面的`key`。
    
    💡 注:修改公钥最后的字符只会影响名字
    
- 回到github上，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，粘贴在你电脑上生成的key。
![](/image/部署Git/部署Git_001.png)

- 为了验证是否成功，在git bash下输入：

```bash
ssh -T git@github.com
```

- 如果是第一次的会提示是否continue，输入yes就会看到：You've successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。
- 设置username和email

```bash
git config --global user.name "your name"
git config --global user.email "your_email@youremail.com"
```

- 进入要上传的仓库，右键git bash，添加远程地址：

```bash
git remote add origin git@github.com:yourName/yourRepo.git
```

### 使用多个密钥

- 1.通过上面方式创建多对密钥和公钥,只不过每次创建需要修改不同名称,防止第二次覆盖
- 2.修改`.ssh`下面的**`config`**文件,按照下面模板每一对密钥和公钥需要配置对应 `Host`和`公钥位置`

![](/image/部署Git/部署Git_002.png)

- 3.更新代码需要把`github.com`替换成 对应配置Host

### 链接与资源

- 图形化客户端
  - [Tower (OSX)](http://www.git-tower.com/)
  - [Source Tree (OSX, 免费)](http://www.sourcetreeapp.com/)
  - [GitBox (OSX, App Store)](https://itunes.apple.com/gb/app/gitbox/id403388357?mt=12)


More info:  [像 git 那样思考](http://think-like-a-git.net/) [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)