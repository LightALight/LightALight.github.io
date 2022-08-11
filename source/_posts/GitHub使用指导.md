---
title: GitHub使用指导
date: 2016-02-13 20:12:32
tags: [git,github]
copyright: true
password:
toc: true
---

GitHub是一个面向开源及私有软件项目的托管平台，因为只支持Git作为唯一的版本库格式进行托管，故名GitHub。文章介绍Git的使用指导。
<!--more-->
## Quick Guide

### 前置

#### 注册

[注册账户](https://github.com/)

### 寻找牛人

- GitHub上的代码库本身：尤其是：[Explore](https://github.com/explore)、[热门关注信息库](https://github.com/popular/watched)两个栏目
- GitHub官方推荐：[GitHub自身的官方博客](https://github.com/blog)与GitHub员工们的个人博客推荐的项目与开发者
- 各类社交媒体上提到的的GitHub库：尤其是[Hacker News上提到的GitHub库](https://hackernews.cc/)。

### 搜索小技巧

| 使用场景 | 使用方法 | 样例 |
| --- | --- | --- |
| 搜索百科大全 | xxx awesome | java awesome |
| 找例子 | xxx simple | java email simple |
| 找空项目架子 | xxx starter | SpringBoot starter |
| 找技术教程 | xxx tutorial | python tutorial |

### 生产力小技巧

#### 给git库做标签

- **codeshelver：**

观察的项目如果多了，怎么管理？用[codeshelver](https://www.codeshelver.com/)，安装扩展之后，可以对GitHub项目做标签。

#### 利用git与github做wiki

- **gollum：**

[gollum](https://github.com/github/gollum)是一个基于git的轻型wiki系统。

#### 监测重点项目

- **GitHubwatcher:**

[GitHubwatcher](https://github.com/DAddYE/githubwatcher)适用于通知不频繁的情景。

#### GitHub官方资源

GitHub官方列出了[一些有用的脚本与书签](http://help.github.com/userscripts-and-bookmarklets/)。

#### 社区驱动的安装与配置文件

GitHub中各类配置文件层出不穷，一些常用的：

- [osh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)：将终端从bash改为zsh之后，可考虑安装社区驱动的zsh配置文件，含有多个插件。可参考旧文[zsh与oh-my-zsh](http://www.yangzhiping.com/tech/zsh-oh-my-zsh.html)
- [gitignore](https://github.com/GitHub/gitignore)：GitHub官方出品
- [yourchili](https://github.com/ericpaulbishop/yourchili):服务器各类安装shell，比如安装nginx等。

### 用途

#### 写作

早在2008年，就有技术图书作者[通过Git来写作](https://github.com/blog/91-not-just-code)，以下是示范：

- [Node.js初学者教材](https://github.com/ManuelKiessling/NodeBeginnerBook)，中文版[在这里](http://www.nodebeginner.org/index-zh-cn.html)。
- [backbone基础](https://github.com/addyosmani/backbone-fundamentals)
- [Sinatra教程](https://github.com/cschneid/sinatra-book)

你能想到的技术前沿话题，大多能在GitHub找到相应的培训材料或者开源图书。

个人写作照样适用。在前文[理想的写作环境：Git+GitHub+Markdown+Jekyll](http://www.yangzhiping.com/tech/writing-space.html)，我已经格外赞美过这些美好事物了。

暖色调的灯光，足够宽度的工作台，听着清脆的键盘声音，基于Git、GitHub、Markdown与Jekyll来写作，不担心写废与排版，只关注最纯粹的写作，是一种享受。我有时候会想，如果Git、Github、Markdown、Jekyll，再加上Yaml、Json的作者，让这些作者们重新来设计今天互联网基础架构偏文本的部分，会诞生一些什么？

#### 个人博客

可以在Github上快速搭建一个基于jekyll的博客系统

- Jekyll：参考[告别wordpress，拥抱jekyll](http://www.yangzhiping.com/tech/wordpress-to-jekyll.html)
- Octopress：参考[Ruby开源项目介绍(1)：octopress——像黑客一样写博客](http://www.yangzhiping.com/tech/octopress.html)
- GitHub Pages：参考[GitHub Pages](http://pages.github.com/)

#### 演讲

借助于GitHub，可以享受更纯粹、更酷的演讲

- 通过[speakerdeck](http://speakerdeck.com/)更好的分享ppt文档
- 使用GitHub著名传教士、Progit作者Scott Chacon开发的[showoff](https://github.com/schacon/showoff)
- 来自开源社区的其他演讲库[impress.js](https://github.com/bartaz/impress.js)

#### 找工作

因为GitHub上的代码无法造假，也容易通过你关注的项目来了解知识面的宽度与深度。现在越来越多知名公司活跃在GitHub，发布开源库并招募各类人才

fredwu是Ruby中文社区活跃份子，他的开源项目[angel_nest](https://github.com/fredwu/angel_nest)，一个天使投资与创业者对接的网站，适合Ruby初学者升级为Ruby中级开发者时学习，也在Hacker News上被[热烈讨论](http://news.ycombinator.com/item?id=2895133)过，让我们来看看他的简历：[http://resume.GitHub.com/?fredwu](http://resume.github.com/?fredwu)


简历生成器:登陆网站[GitHub简历生成器](http://resume.github.com/)，填入你的GitHub网站用户名即可。

第三方网站提供基于GitHub的人才招聘服务，例如：

- [GitHire](http://githire.com/):通过它，可以找出你所在地区的程序员。
- [Gitalytics.com](http://www.gitalytics.com/)：通过它，能评估某位程序员在GitHub、LinkedIn、StackOverflow、hackernews等多个网站的影响力。

### 链接与资源

- 图形化客户端
  - [GitHub for Mac (OSX, 免费)](http://mac.github.com/)
- 指南和手册
  - [GitHub 帮助](http://help.github.com/)


More info: [Github 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html) [如何高效利用GitHub](http://www.yangzhiping.com/tech/github.html)