---
title: 部署Docker
date: 2018-07-23 21:32:11
tags: [环境部署,docker]
copyright: true
password:
toc: true
---

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。文章介绍如何在居于Centos7.5安装Docker CE(社区免费版)。
<!--more-->
## Quick Guide

### 安装
* 1.前提条件:Docker 运行在 CentOS 7 上，要求系统为64位且系统内核版本为 3.10 以上。
    ```bash
    uname -r
    ```
    ![](/image/部署Docker_001.png)

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
    ![](/image/部署Docker_002.png)

* 9.查看docker信息
    ```bash
    docker version # 查看docker的版本号，包括客户端、服务端、依赖的Go等
    docker info # 查看系统(docker)层面信息，包括管理的images, containers数等
    ```


### 关于镜像、容器、仓库的基本命令

![](/image/部署Docker_003.png)

#### 基本概念

* 镜像（Image）类似于虚拟机的镜像，可以将他理解为一个面向Docker引擎的只读模板，包含了文件系统
* 容器（Container）类似于一个轻量级的沙箱子，是镜像的一个运行实例，但它带有额外的可写层
* 仓库（Repository）类似与代码仓库，是Docker集中存放镜像文件的场所


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


More info: [Docker安装手册](https://docs.docker-cn.com/engine/installation/)
