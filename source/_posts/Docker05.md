---
title: Docker（五）Docker Machine
date: 2018-10-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---

 [Docker Machine](https://docs.docker.com/machine/overview/) 是 Docker 官方提供的一个工具，它可以帮助我们在远程的机器上安装 Docker，或者在虚拟机 host 上直接安装虚拟机并在虚拟机中安装 Docker。 本文章介绍如何使用 Docker  Machine 。

<!--more-->

## Quick Guide


### Docker Machine

Docker Machine是一个工具，可让您在虚拟主机上安装Docker Engine，并使用docker-machine命令管理主机。

- Docker Engine：人们说的“Docker”通常指的是Docker Engine，由Docker守护程序组成的客户端 - 服务器应用程序，指定用于与守护进程交互的接口的REST API，以及与守护进程通信的命令行界面（CLI）客户端（通过REST API包装器）。

	![](/image/Docker05/Docker05_001.png)

	![](/image/Docker05/Docker05_002.png)

- Docker Machine是一个用于配置和管理Dockerized主机（带有Docker Engine的主机）的工具。	     
	Docker Machine有自己的命令行客户端 docker-machine和Docker Engine客户端。
	使用Machine在一个或多个虚拟系统上安装Docker Engine，这些虚拟系统可以是本地的（使用Machine在Mac或Windows上的VirtualBox中安装和运行Docker Engine）或远程（使用Machine在云提供商上配置Dockerized主机）。
	这些Dockerized机器就是托管在 Docker Machine上的机器。

	![](/image/Docker05/Docker05_003.png)

### 安装 Docker Machine

安装 Docker Machine 之前你需要先安装 Docker。

Docker Mechine 可以在多种平台上安装使用，包括 Linux 、MacOS 以及 windows。

#### Linux 安装命令

```bash
$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
  sudo mv /tmp/docker-machine /usr/local/bin/docker-machine &&
  chmod +x /usr/local/bin/docker-machine
```

#### macOS 安装命令

```bash
$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/usr/local/bin/docker-machine &&
  chmod +x /usr/local/bin/docker-machine
```

#### Windows 安装命令

如果你是 Windows 平台，可以使用 [Git BASH](https://git-for-windows.github.io/)，并输入以下命令：

```bash
$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  mkdir -p "$HOME/bin" &&
  curl -L $base/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe" &&
  chmod +x "$HOME/bin/docker-machine.exe"
```

查看是否安装成功：

```bash
$ docker-machine version
docker-machine version 0.16.0, build 9371605
```
---------
### 在远程主机上安装 Docker

如果我们有多台 Ubuntu 主机都需要安装 Docker，不需要一个个登录安装，通过 docker-machine 命令我们可以轻松的在远程主机上安装 Docker。


#### 1.前提条件

在使用 docker-machine 进行远程安装前我们需要做一些准备工作：
- 1.在目标主机上创建一个用户并加入sudo 组
	```bash
	# 比如我们要在远程主机上添加一个名为 nick 的用户并加入 sudo 组
	$ sudo adduser nick
	$ sudo usermod -a -G sudo nick
	```

- 2.为该用户设置 sudo 操作不需要输入密码

    ```bash
    # 打开/etc/sudoers
    sudo visudo
    # 把下面一行内容添加到文档的最后并保存文件
    nick   ALL=(ALL:ALL) NOPASSWD: ALL
    ```

  

- 3.把本地用户的 ssh public key 添加到目标主机上

  ```bash
  $ ssh-copy-id -i ~/.ssh/id_rsa.pub nick@xxx.xxx.xxx.xxx
  ```

#### 2.安装



在本地运行下面的命令：
```bash
# generic驱动
$ docker-machine create -d generic \
    --generic-ip-address=xxx.xxx.xxx.xxx \
    --generic-ssh-user=nick \
    --generic-ssh-key ~/.ssh/id_rsa \
    krdevdb
```

- create 命令本是要创建虚拟主机并安装 Docker，因为本例中的目标主机已经存在，所以仅安装 Docker。
- -d 是 --driver 的简写形式，主要用来指定使用什么驱动程序来创建目标主机。
- --generic 开头的三个参数主要是指定操作的目标主机和使用的账户。
- krdevdb 是虚拟机的名称，Docker Machine 会用它来设置目标主机的名称。

![](/image/Docker05/Docker05_004.png)

#### 3.检查安装结果

```bash
$ docker-machine ls
```
![](/image/Docker05/Docker05_005.png)

#### 4.管理远程的 Docker

```bash
# 远程到主机krdevdb
eval $(docker-machine env krdevdb) 
# 查看版本
docker version
```

![](/image/Docker05/Docker05_006.png)



#### 5.在本地主机上安装带有 Docker 的虚机
在本地的一台安装了 vSphere 的虚拟机 host 上安装带有 Docker 的虚拟机。

```bash
$ docker-machine create \
    --driver vmwarevsphere \
    --vmwarevsphere-vcenter=xxx.xxx.xxx.xxx \
    --vmwarevsphere-username=root \
    --vmwarevsphere-password=12345678 \
    --vmwarevsphere-cpu-count=1 \
    --vmwarevsphere-memory-size=512 \
    --vmwarevsphere-disk-size=10240 \
    testvm
```

解释一下比较重要的参数：

- --driver vmwarevsphere ：我们的虚拟机 host 上安装的是 vmware 的产品 vSphere，因此需要给 Docker Machine 提供对应的驱动，这样才能够在上面安装新的虚拟机。
- --vmwarevsphere-vcenter=xxx.xxx.xxx.xxx ：虚拟机 host 的 IP 地址
- --vmwarevsphere-username=root ：虚拟机 host 的 用户名
- --vmwarevsphere-password=12345678 ：虚拟机 host 的 密码
- --vmwarevsphere-cpu-count=1 ：虚拟机 host 的 cpu
- --vmwarevsphere-memory-size=512 ：虚拟机 host 的 内存
- --vmwarevsphere-disk-size=10240 ：虚拟机 host 的 磁盘资源
- testvm：新建虚拟机的名称。

------




### 常用命令


- 1.列出可用的机器

    ```bash
    $ docker-machine ls
    ```


- 2.创建机器

    ```bash
    $ docker-machine create --driver virtualbox test
    ```

	- **--driver**：指定用来创建机器的驱动类型，这里是 virtualbox。



- 3.查看机器的 ip

    ```bash
    $ docker-machine ip test
    ```

- 4.停止机器

    ```bash
    $ docker-machine stop test
    ```
- 5.启动机器

    ```bash
    $ docker-machine start test
    ```


- 6.进入机器

    ```bash
    $ docker-machine ssh test
    ```
    
------

### 命令参数说明

- **docker-machine active**：查看当前激活状态的 Docker 主机。

  ```bash
  $ docker-machine ls
  
  NAME      ACTIVE   DRIVER         STATE     URL
  dev       -        virtualbox     Running   tcp://192.168.99.103:2376
  staging   *        digitalocean   Running   tcp://203.0.113.81:2376
  
  $ echo $DOCKER_HOST
  tcp://203.0.113.81:2376
  
  $ docker-machine active
  staging
  ```

- **config**：查看当前激活状态 Docker 主机的连接信息。

- **creat**：创建 Docker 主机

- **env**：显示连接到某个主机需要的环境变量

- **inspect**： 以 json 格式输出指定Docker的详细信息

- **ip**： 获取指定 Docker 主机的地址

- **kill**： 直接杀死指定的 Docker 主机

- **ls**： 列出所有的管理主机

- **provision**： 重新配置指定主机

- **regenerate-certs**： 为某个主机重新生成 TLS 信息

- **restart**： 重启指定的主机

- **rm**： 删除某台 Docker 主机，对应的虚拟机也会被删除

- **ssh**： 通过 SSH 连接到主机上，执行命令

- **scp**： 在 Docker 主机之间以及 Docker 主机和本地主机之间通过 scp 远程复制数据

- **mount**： 使用 SSHFS 从计算机装载或卸载目录

- **start**： 启动一个指定的 Docker 主机，如果对象是个虚拟机，该虚拟机将被启动

- **status**： 获取指定 Docker 主机的状态(包括：Running、Paused、Saved、Stopped、Stopping、Starting、Error)等

- **stop**： 停止一个指定的 Docker 主机

- **upgrade**： 将一个指定主机的 Docker 版本更新为最新

- **url**： 获取指定 Docker 主机的监听 URL

- **version**： 显示 Docker Machine 的版本或者主机 Docker 版本

- **help**： 显示帮助信息