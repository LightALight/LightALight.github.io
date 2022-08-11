---
title: Docker（二）Docker的运行
date: 2018-07-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---

文章介绍Docker的如何运行和基本命令。
<!--more-->

## Quick Guide

### Docker的构成

Docker有三个组件和三个基本元素:

三个组件分别是：

 - **Docker Client** ：是用户界面，它支持用户与 **Docker Daemon** 之间通信。 
 - **Docker Daemon**： 运行于主机上，处理服务请求。 
 - **Docker Registry**：是中央registry，拥有Docker容器镜像备份的公有和私有访问权限。


 三个基本要素分别是： 
 - **Docker Containers**： 负责应用程序的运行，包括操作系统、用户添加的文件以及元数据。 镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
 - **Docker Images**： 是一个只读模板，用来运行Docker容器。 就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
 - **DockerFile** ：是文件指令集，用来说明如何自动创建Docker镜像。 


![](/image/Docker02/Docker02_001.png)

### Docker的技术支柱

Docker使用以下操作系统的功能来提高容器技术效率：

 - **Namespaces** 充当隔离的第一级。确保一个容器中运行一个进程而且不能看到或影响容器外的其它进程。 
 - **Control Groups**是LXC的重要组成部分，具有资源核算与限制的关键功能。 
 - **UnionFS**（文件系统）作为容器的构建块。为了支持Docker的轻量级以及速度快的特性，它创建了用户层。 



### 使用Docker 运行程序


#### 1.创建镜像


- 1.1.Docker Client 发送给Docker Daemon命令:需要创建的镜像以及需要在容器内运行的命令

  ```bash
  docker build -t ubuntu:15.10 .
  ```

  各个参数解析：

  - **docker:** Docker 的二进制执行文件。
  - **run:** 与前面的 docker 组合来创建镜像 。
  - **ubuntu:15.10** 指定要创建的镜像名称:镜像标签 
  - **.**  指定镜像构建过程中的上下文环境的目录 

  

- 1.2.镜像创建完成，就可以将它们推送到中央Registry：Docker Registry，以供他人使用。Docker Index为镜像提供了两个级别的访问权限：公有访问和私有访问。公有仓库是可搜索和可重复使用的，而私有仓库只能给那些拥有访问权限的成员使用.你可以将镜像存储在私有仓库，Docker官网有私有仓库的套餐可以供你选择。

  ```shell
  # 仓库地址在 /etc/docker 下的daemon.json文件下可以找到
  docker login # 登陆仓库
  docker tag ubuntu:15.10 <仓库地址>/ubuntu:15.10 # 修改镜像标签
  docker push <仓库地址>/ubuntu:15.10 # 镜像推送
  ```

#### 2.运行容器

运行容器源于我们在第一步中创建的镜像。当容器被启动后，一个读写层会被添加到镜像的顶层。当分配到合适的网络和IP地址后，需要的应用程序就可以在容器中运行了。 

```shell
docker run ubuntu:15.10 /bin/echo "Hello world"
```

各个参数解析：

- **docker:** Docker 的二进制执行文件。
- **run:** 与前面的 docker 组合来运行一个容器。
- **ubuntu:15.10** 指定要运行的镜像，Docker 首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 **Docker Hub** 下载公共镜像。
- **/bin/echo "Hello world":** 在启动的容器里执行的命令



### 关于镜像、容器、仓库的基本命令

![](/image/Docker02/Docker02_002.png)


#### 镜像

* 1.获取镜像
  
    ```bash
    docker search <image> # 在docker index中搜索image
    ```

* 2.获取镜像
    ```bash
    docker pull <image>  # 从docker registry server 中下拉image
    docker pull <server:port/image:tag> # 获取image
	```

* 3.查看镜像
    ```bash
    docker images： # 列出images
    docker images -a # 列出所有的images（包含历史）
    ```

* 4.删除镜像
    ```bash
    docker rmi  <image ID> # 删除一个或多个image
    ```

* 5.创建镜像
    ```bash
     docker commit -m "add new image" -a <container_id> <new_image_name> # 基于已有镜像的容器创建
     cat <本地模板> | Docker import - image:tag # 基于本地模板导入
     docker build -t <image:tag> <docker_file_dir. # 基于dockerfile创建
    ```

* 6.存出镜像
    ```bash
    docker save -o <image_file> <image:tag>
    ```

* 7.载入镜像
    ```bash
    docker save -o <image_file> <image:tag>
    ```

* 8.上传镜像
    ```bash
    docker push <user/image:tag>
    ```


#### 容器

* 1.创建容器
    ```bash
    docker create -it <image:tag>
    ```

* 2.创建并启动容器
    ```bash
    docker run -it <image:tag> /bin/bash
    ```

* 3.守护态运行
    ```bash
    ddocker run -d <image:tag>
    ```

* 4.查看容器信息
    ```bash
    docker ps # 列出当前所有正在运行的container
    docker ps -l # 列出最近一次启动的container
    docker ps -a # 列出所有的container（包含历史，即运行过的container）
    docker ps -q # 列出最近一次运行的container ID
    ```

* 5.获取容器的输出信息
    ```bash
    docker logs -f <image:tag>或<container_id>
    ```

* 6.终止容器
    ```bash
    docker stop <image:tag>或<container_id>
    ```

* 7.启动容器
    ```bash
    docker start <image:tag>或<container_id>
    ```

* 8.重启容器

    ```bash
    docker restart <image:tag>或<container_id>
    ```

* 9.进入容器
    ```bash
    docker attach <image:tag>或<container_id>
    docker exec -it <image:tag>或<container_id> /bin/bash 
    nsenter --target <docker_pid> --mount --uts --ipc --net --pid
    ```

* 10.删除容器
    ```bash
    docker rm <container_id> #：删除一个或多个container
    docker rm `docker ps -a -q` #：删除所有的container
    docker ps -a -q | xargs docker rm # 同上, 删除所有的container
    ```

* 11.导出容器
    ```bash
    docker export <container_id> >test.tar
    ```

* 12.容器快照导入到本地镜像库
    ```bash
    cat <container_snapshot> | docker import - <user/image:tag>
    ```

#### 仓库

* 1.登录
    ```bash
    docker login
    ```

* 2.更新镜像标签
    ```bash
    docker tag <server:port/image:tag> <image:tag>
    ```

* 3.创建私有仓库
    ```bash
    docker run -p 5000:5000 registry:<registry_version>
    ```

* 4.管理私有仓库镜像
    ```bash
    docker tag <image:tag> <私有仓库IP:端口/new_tag> # 重新标记一个本地镜像为私有仓库的版本
    docker push <私有仓库IP:端口/image:new_tag>
    curl http://<私有仓库IP:端口>/v2/<image>/tags/list # 查看私有仓库中的镜像列表
    docker pull <私有仓库IP:端口/image:new_tag> # 拉取本地仓库中的镜像
    ```

More info: [Docker教程](https://www.flux7.com/tutorial/docker-tutorial-series-part-1-an-introduction-docker-components/)
