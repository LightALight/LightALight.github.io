---
title: Docker（一）Docker的基本概念
date: 2018-06-16 21:32:11
tags: docker
copyright: true
password:
toc: true

---

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。文章介绍 Docker 的基本概念和部署安装。

<!--more-->

## Quick Guide

### Linux 容器

资源利用率和环境部署的问题，早期使用虚拟机解决。但是虚拟机存在问题（资源占用多、冗余步骤多、启动慢），由于虚拟机存在这些缺点，Linux 发展出了另一种虚拟化技术：**Linux 容器（Linux Containers，缩写为 LXC）**。

**Linux 容器不是模拟一个完整的操作系统，而是对进程进行隔离**。或者说，在正常进程的外面套了一个保护层。对于容器里面的进程来说，它接触到的各种资源都是虚拟的，从而实现与底层系统的隔离。


### 容器优势

![](/image/Docker01/Docker01_001.png)


- 启动快

容器里面的应用，直接就是底层系统的一个进程，而不是虚拟机内部的进程。所以，启动容器相当于启动本机的一个进程，而不是启动一个操作系统，速度就快很多。

- 资源占用少

容器只占用需要的资源，不占用那些没有用到的资源；虚拟机由于是完整的操作系统，不可避免要占用所有资源。另外，多个容器可以共享资源，虚拟机都是独享资源。

- 体积小

容器只要包含用到的组件即可，而虚拟机是整个操作系统的打包，所以容器文件比虚拟机文件要小很多。

![](/image/Docker01/Docker01_002.png)


### Docker

Docker 属于 Linux 容器的一种封装，提供简单易用的容器使用接口。它是目前最流行的 Linux 容器解决方案。

Docker 将应用程序与该程序的依赖，打包在一个文件里面。运行这个文件，就会生成一个虚拟容器。程序在这个虚拟容器里运行，就好像在真实的物理机上运行一样。



### Docker 的用途

Docker 的主要用途，目前有三大类。

 - 提供一次性的环境。比如本地测试他人的软件、持续集成的时候提供单元测试和构建的环境。
 - 提供弹性的云服务。因为 Docker 容器可以随开随关，很适合动态扩容和缩容。
 - 组建微服务架构。通过多个容器，一台机器可以跑多个服务，因此在本机就可以模拟出微服务架构。



![](/image/Docker01/Docker01_003.png)

### Docker 框架

Docker 包括三个基本概念:

- 镜像（Image）：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
- 容器（Container）：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
- 仓库（Repository）：仓库可看成一个代码控制中心，用来保存镜像。
- 
Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。Docker 容器通过 Docker 镜像来创建。




![](/image/Docker01/Docker01_004.png)


|          概念          | 说明                                                         |
| :--------------------: | :----------------------------------------------------------- |
|  Docker 镜像(Images)   | Docker 镜像是用于创建 Docker 容器的模板，比如 Ubuntu 系统。  |
| Docker 容器(Container) | 容器是独立运行的一个或一组应用，是镜像运行时的实体。         |
| Docker 客户端(Client)  | Docker 客户端通过命令行或者其他工具使用 Docker SDK (https://docs.docker.com/develop/sdk/) 与 Docker 的守护进程通信。 |
|   Docker 主机(Host)    | 一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。       |
|    Docker Registry     | Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。一个 Docker Registry 中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本。我们可以通过 **<仓库名>:<标签>** 的格式来指定具体是这个软件哪个版本的镜像。如果不给出标签，将以 **latest** 作为默认标签。**Docker Hub**([https://hub.docker.com](https://hub.docker.com/)) 官方维护一个公共仓库，提供了庞大的镜像集合，使用需要先注册一下。 |
|     Docker Machine     | Docker Machine是一个简化Docker安装的命令行工具，通过一个简单的命令行即可在相应的平台上安装Docker，比如VirtualBox、 Digital Ocean、Microsoft Azure。 |





### Docker 部署安装

Docker 是一个开源的商业产品，有两个版本：社区版（Community Edition，缩写为 CE）和企业版（Enterprise Edition，缩写为 EE）。企业版包含了一些收费服务，个人开发者一般用不到。
Docker CE 的安装请参考官方文档。

> - [Mac](https://docs.docker.com/docker-for-mac/install/)
> - [Windows](https://docs.docker.com/docker-for-windows/install/)
> - [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
> - [Debian](https://docs.docker.com/install/linux/docker-ce/debian/)
> - [CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
> - [Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)
> - [其他 Linux 发行版](https://docs.docker.com/install/linux/docker-ce/binaries/)


#### 安装步骤

* 1.前提条件:Docker 运行在 CentOS 7 上，要求系统为64位且系统内核版本为 3.10 以上。
    ```bash
    uname -r
    ```
    ![](/image/Docker01/Docker01_005.png)

* 2.移除旧的版本
    ```bash
    sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
    ```

* 3.安装必要的系统工具
    ```bash
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    ```

* 4.添加软件源信息
    ```bash
    sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    ```

* 5.更新 yum 缓存
    ```bash
    sudo yum makecache fast
    ```

* 6.安装
    ```bash
    sudo yum -y install docker-ce
    ```

* 7.启动 Docker 后台服务
    ```bash
    sudo systemctl start docker
    ```

* 8.测试运行 hello-world
    ```bash
    docker run hello-world
    ```
    ![](/image/Docker01/Docker01_006.png)

* 9.查看docker信息
    ```bash
    docker version # 查看docker的版本号，包括客户端、服务端、依赖的Go等
    docker info # 查看系统(docker)层面信息，包括管理的images, containers数等
    ```

### Docker 资源汇总


#### Docker 资源

- Docker 官方主页: [https://www.docker.com](https://www.docker.com/)
- Docker 官方博客: https://blog.docker.com/
- Docker 官方文档: https://docs.docker.com/
- Docker Store: [https://store.docker.com](https://store.docker.com/)
- Docker Cloud: [https://cloud.docker.com](https://cloud.docker.com/)
- Docker Hub: [https://hub.docker.com](https://hub.docker.com/)
- Docker 的源代码仓库: https://github.com/moby/moby
- Docker 发布版本历史: https://docs.docker.com/release-notes/
- Docker 常见问题: https://docs.docker.com/engine/faq/
- Docker 远端应用 API: https://docs.docker.com/develop/sdk/

#### Docker 国内镜像

- 阿里云的加速器：https://help.aliyun.com/document_detail/60750.html
- 网易加速器：http://hub-mirror.c.163.com
- 官方中国加速器：https://registry.docker-cn.com
- ustc 的镜像：https://docker.mirrors.ustc.edu.cn
- daocloud：https://www.daocloud.io/mirror#accelerator-doc（注册后使用）



More info: [Docker教程]( https://www.runoob.com/docker/docker-architecture.html )