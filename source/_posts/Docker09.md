---
title: Docker（九）Docker 命令
date: 2019-02-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---


在本章介绍 Docker 命令。


<!--more-->

## Quick Guide

### 容器生命周期管理

#### run

docker run ：创建一个新的容器并运行一个命令

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

OPTIONS说明：

- **-a stdin:** 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；
- **-d:** 后台运行容器，并返回容器ID；
- **-i:** 以交互模式运行容器，通常与 -t 同时使用；
- **-P:** 随机端口映射，容器内部端口**随机**映射到主机的端口
- **-p:** 指定端口映射，格式为：**主机(宿主)端口:容器端口**
- **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
- **--name="nginx-lb":** 为容器指定一个名称；
- **--dns 8.8.8.8:** 指定容器使用的DNS服务器，默认和宿主一致；
- **--dns-search example.com:** 指定容器DNS搜索域名，默认和宿主一致；
- **-h "mars":** 指定容器的hostname；
- **-e username="ritchie":** 设置环境变量；
- **--env-file=[]:** 从指定文件读入环境变量；
- **--cpuset="0-2" or --cpuset="0,1,2":** 绑定容器到指定CPU运行；
- **-m :** 设置容器使用内存最大值；
- **--net="bridge":** 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；
- **--link=[]:** 添加链接到另一个容器；
- **--expose=[]:** 开放一个端口或一组端口；
- **--volume , -v:** 绑定一个卷



```bash
# 使用docker镜像nginx:latest以后台模式启动一个容器,并将容器命名为mynginx。
docker run --name mynginx -d nginx:latest
```

#### start/stop/restart 

**docker start** :启动一个或多个已经被停止的容器

**docker stop** :停止一个运行中的容器

**docker restart** :重启容器

```bash
docker start [OPTIONS] CONTAINER [CONTAINER...]
docker stop [OPTIONS] CONTAINER [CONTAINER...]
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

```bash
# 启动已被停止的容器myrunoob
docker start myrunoob
# 停止运行中的容器myrunoob
docker stop myrunoob
# 重启容器myrunoob
docker restart myrunoob
```

#### kill

**docker kill** :杀掉一个运行中的容器。


```bash
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

OPTIONS说明：

- **-s :** 向容器发送一个信号

```bash
# 杀掉运行中的容器mynginx
runoob@runoob:~$ docker kill -s KILL mynginx
```

#### rm

**docker rm ：** 删除一个或多个容器。


```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

OPTIONS说明：

- **-f :** 通过 SIGKILL 信号强制删除一个运行中的容器。
- **-l :** 移除容器间的网络连接，而非容器本身。
- **-v :** 删除与容器关联的卷。


```bash
# 强制删除容器 db01、db02
docker rm -f db01 db02
```


#### pause/unpause

**docker pause** :暂停容器中所有的进程。

**docker unpause** :恢复容器中所有的进程。

```bash
docker pause [OPTIONS] CONTAINER [CONTAINER...]
docker unpause [OPTIONS] CONTAINER [CONTAINER...]
```


```bash
# 暂停数据库容器db01提供服务。
docker pause db01
# 恢复数据库容器db01提供服务。
docker unpause db01
```


#### create

**docker create ：** 创建一个新的容器但不启动它


```bash
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

```bash
# 使用docker镜像nginx:latest创建一个容器,并将容器命名为myrunoob
runoob@runoob:~$ docker create  --name myrunoob  nginx:latest      
```


#### exec

**docker exec ：** 在运行的容器中执行命令

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

OPTIONS说明：

- **-d :** 分离模式: 在后台运行
- **-i :** 即使没有附加也保持STDIN 打开
- **-t :** 分配一个伪终端


```bash
# 在容器 mynginx 中以交互模式执行容器内 /root/runoob.sh 脚本:
runoob@runoob:~$ docker exec -it mynginx /bin/sh /root/runoob.sh
# 在容器 mynginx 中开启一个交互模式的终端:
runoob@runoob:~$ docker exec -i -t  mynginx /bin/bash
```


----------
### 容器操作

#### ps

**docker ps :** 列出容器


```bash
docker ps [OPTIONS]
```

OPTIONS说明：

- **-a :**显示所有的容器，包括未运行的。
- **-f :**根据条件过滤显示的内容。
- **--format :**指定返回值的模板文件。
- **-l :**显示最近创建的容器。
- **-n :**列出最近创建的n个容器。
- **--no-trunc :**不截断输出。
- **-q :**静默模式，只显示容器编号。
- **-s :**显示总的文件大小。


```bash
# 列出所有在运行的容器信息
runoob@runoob:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                ...  PORTS                    NAMES
09b93464c2f7   nginx:latest   "nginx -g 'daemon off" ...  80/tcp, 443/tcp          myrunoob
96f7f14e99ab   mysql:5.6      "docker-entrypoint.sh" ...  0.0.0.0:3306->3306/tcp   mymysql
```
输出详情介绍：
- **CONTAINER ID:** 容器 ID。
- **IMAGE:** 使用的镜像。
- **COMMAND:** 启动容器时运行的命令。
- **CREATED:** 容器的创建时间。
- **STATUS:** 容器状态。
- **PORTS:** 容器的端口信息和使用的连接类型（tcp\udp）。
- **NAMES:** 自动分配的容器名称。

状态有7种：
- created（已创建）
- restarting（重启中）
- running（运行中）
- removing（迁移中）
- paused（暂停）
- exited（停止）
- dead（死亡）



#### inspect

**docker inspect :** 获取容器/镜像的元数据。

```bash
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

OPTIONS说明：

- **-f :**指定返回值的模板文件。
- **-s :**显示总的文件大小。
- **--type :**为指定类型返回JSON。


```bash
# 获取镜像mysql:5.6的元信息。

runoob@runoob:~$ docker inspect mysql:5.6
[
    {
        "Id": "sha256:2c0964ec182ae9a045f866bbc2553087f6e42bfc16074a74fb820af235f070ec",
        "RepoTags": [
            "mysql:5.6"
        ],
        "RepoDigests": [],
        "Parent": "",
        "Comment": "",
        "Created": "2016-05-24T04:01:41.168371815Z",
        "Container": "e0924bc460ff97787f34610115e9363e6363b30b8efa406e28eb495ab199ca54",
        "ContainerConfig": {
            "Hostname": "b0cf605c7757",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "3306/tcp": {}
            },
...
```

```bash
# 获取正在运行的容器mymysql的 IP。
runoob@runoob:~$ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mymysql
172.17.0.3
```

#### top

**docker top :**查看容器中运行的进程信息，支持 ps 命令参数。


```bash
docker top [OPTIONS] CONTAINER [ps OPTIONS]
```

```bash
# 查看容器mymysql的进程信息。
runoob@runoob:~/mysql$ docker top mymysql
UID    PID    PPID    C      STIME   TTY  TIME       CMD
999    40347  40331   18     00:58   ?    00:00:02   mysqld
```

#### attach

**docker attach :**连接到正在运行中的容器。

### 语法

```bash
docker attach [OPTIONS] CONTAINER
```


```bash
# 容器mynginx将访问日志指到标准输出，连接到容器查看访问信息。
runoob@runoob:~$ docker attach --sig-proxy=false mynginx
192.168.239.1 - - [10/Jul/2016:16:54:26 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.93 Safari/537.36" "-"
```

#### events

**docker events :** 从服务器获取实时事件

```bash
docker events [OPTIONS]
```

OPTIONS说明：
- **-f ：**根据条件过滤事件；
- **--since ：**从指定的时间戳后显示所有事件;
- **--until ：**流水时间显示到指定的时间为止；



```bash
# 显示docker 2016年7月1日后的所有事件。
runoob@runoob:~/mysql$ docker events  --since="1467302400"
2016-07-08T19:44:54.501277677+08:00 network connect 66f958fd13dc4314ad20034e576d5c5eba72e0849dcc38ad9e8436314a4149d4 (container=b8573233d675705df8c89796a2c2687cd8e36e03646457a15fb51022db440e64, name=bridge, type=bridge)
2016-07-08T19:44:54.723876221+08:00 container start b8573233d675705df8c89796a2c2687cd8e36e03646457a15fb51022db440e64 (image=nginx:latest, name=elegant_albattani)
2016-07-08T19:44:54.726110498+08:00 container resize b8573233d675705df8c89796a2c2687cd8e36e03646457a15fb51022db440e64 (height=39, image=nginx:latest, name=elegant_albattani, width=167)
2016-07-08T19:46:22.137250899+08:00 container die b8573233d675705df8c89796a2c2687cd8e36e03646457a15fb51022db440e64 (exitCode=0, image=nginx:latest, name=elegant_albattani)
...
```

#### logs

**docker logs :** 获取容器的日志

```bash
docker logs [OPTIONS] CONTAINER
```

OPTIONS说明：
- **-f :** 跟踪日志输出
- **--since :**显示某个开始时间的所有日志
- **-t :** 显示时间戳
- **--tail :**仅列出最新N条容器日志



```bash
# 跟踪查看容器mynginx的日志输出。
runoob@runoob:~$ docker logs -f mynginx
192.168.239.1 - - [10/Jul/2016:16:53:33 +0000] "GET / HTTP/1.1" 200 612 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.93 Safari/537.36" "-"
2016/07/10 16:53:33 [error] 5#5: *1 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 192.168.239.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "192.168.239.130", referrer: "http://192.168.239.130/"
192.168.239.1 - - [10/Jul/2016:16:53:33 +0000] "GET /favicon.ico HTTP/1.1" 404 571 "http://192.168.239.130/" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.93 Safari/537.36" "-"
192.168.239.1 - - [10/Jul/2016:16:53:59 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.93 Safari/537.36" "-"
...
```


#### wait

**docker wait :** 阻塞运行直到容器停止，然后打印出它的退出代码。


```bash
docker wait [OPTIONS] CONTAINER [CONTAINER...]
```

```bash
docker wait CONTAINER
```

#### export

**docker export :**将文件系统作为一个tar归档文件导出到STDOUT。


```bash
docker export [OPTIONS] CONTAINER
```
OPTIONS说明：
- **-o :**将输入内容写到文件。



```bash
# 将id为a404c6c174a2的容器按日期保存为tar文件。
runoob@runoob:~$ docker export -o mysql-`date +%Y%m%d`.tar a404c6c174a2
runoob@runoob:~$ ls mysql-`date +%Y%m%d`.tar
mysql-20160711.tar
```

#### port

**docker port :**列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。


```bash
docker port [OPTIONS] CONTAINER [PRIVATE_PORT[/PROTO]]
```

```bash
# 查看容器mynginx的端口映射情况。
runoob@runoob:~$ docker port mymysql
3306/tcp -> 0.0.0.0:3306
```

----------
### 容器rootfs命令

#### commit

**docker commit :**从容器创建一个新的镜像。


```bash
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

OPTIONS说明：
- **-a :**提交的镜像作者；
- **-c :**使用Dockerfile指令来创建镜像；
- **-m :**提交时的说明文字；
- **-p :**在commit时，将容器暂停。


```bash
# 将容器a404c6c174a2 保存为新的镜像,并添加提交人信息和说明信息。
runoob@runoob:~$ docker commit -a "runoob.com" -m "my apache" a404c6c174a2  mymysql:v1 
sha256:37af1236adef1544e8886be23010b66577647a40bc02c0885a6600b33ee28057
```

#### cp

**docker cp :**用于容器与主机之间的数据拷贝。

### 语法

```bash
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
```

OPTIONS说明：
- **-L :**保持源目标中的链接

```bash
# 将主机/www/runoob目录拷贝到容器96f7f14e99ab的/www目录下。
docker cp /www/runoob 96f7f14e99ab:/www/
```

#### diff

**docker diff :** 检查容器里文件结构的更改。


```bash
docker diff [OPTIONS] CONTAINER
```

```bash
# 查看容器mymysql的文件结构更改。
runoob@runoob:~$ docker diff mymysql
A /logs
```



### 镜像仓库

#### login

**docker login :** 登陆到一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub

**docker logout :** 登出一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub


```bash
docker login [OPTIONS] [SERVER]
docker logout [OPTIONS] [SERVER]
```
OPTIONS说明：
- **-u :**登陆的用户名
- **-p :**登陆的密码


```bash
# 登陆到Docker Hub
docker login -u 用户名 -p 密码
# 登出Docker Hub
docker logout
```

#### pull

**docker pull :** 从镜像仓库中拉取或者更新指定镜像


```bash
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

OPTIONS说明：
- **-a :**拉取所有 tagged 镜像  
- **--disable-content-trust :**忽略镜像的校验,默认开启


```bash
# 从Docker Hub下载java最新版镜像。
docker pull java
```

#### push

**docker push :** 将本地的镜像上传到镜像仓库,要先登陆到镜像仓库

```bash
docker push [OPTIONS] NAME[:TAG]
```

OPTIONS说明：
- **--disable-content-trust :**忽略镜像的校验,默认开启


```bash
# 上传本地镜像myapache:v1到镜像仓库中。
docker push myapache:v1
```


#### search

**docker search :** 从Docker Hub查找镜像


```bash
docker search [OPTIONS] TERM
```

OPTIONS说明：
- **--automated :**只列出 automated build类型的镜像；
- **--no-trunc :**显示完整的镜像描述；
- **-s :**列出收藏数不小于指定值的镜像。


```bash
# 从Docker Hub查找所有镜像名包含java，并且收藏数大于10的镜像
runoob@runoob:~$ docker search -s 10 java
NAME                  DESCRIPTION                           STARS   OFFICIAL   AUTOMATED
java                  Java is a concurrent, class-based...   1037    [OK]       
anapsix/alpine-java   Oracle Java 8 (and 7) with GLIBC ...   115                [OK]
develar/java                                                 46                 [OK]
isuper/java-oracle    This repository contains all java...   38                 [OK]
lwieske/java-8        Oracle Java 8 Container - Full + ...   27                 [OK]
nimmis/java-centos    This is docker images of CentOS 7...   13                 [OK]
```

参数说明：
- **NAME:** 镜像仓库源的名称
- **DESCRIPTION:** 镜像的描述
- **OFFICIAL:** 是否 docker 官方发布
- **stars:** 类似 Github 里面的 star，表示点赞、喜欢的意思。
- **AUTOMATED:** 自动构建。


----------
### 本地镜像管理

#### images

**docker images :** 列出本地镜像。


```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

OPTIONS说明：

- **-a :**列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层）；
- **--digests :**显示镜像的摘要信息；
- **-f :**显示满足条件的镜像；
- **--format :**指定返回值的模板文件；
- **--no-trunc :**显示完整的镜像信息；  
- **-q :**只显示镜像ID。



```bash
# 查看本地镜像列表
runoob@runoob:~$ docker images
```

#### rmi

**docker rmi :** 删除本地一个或多少镜像。


```bash
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

OPTIONS说明：
- **-f :**强制删除；
- **--no-prune :**不移除该镜像的过程镜像，默认移除；


```bash
# 强制删除本地镜像 runoob/ubuntu:v4
root@runoob:~# docker rmi -f runoob/ubuntu:v4
```

#### tag

**docker tag :** 标记本地镜像，将其归入某一仓库。

```bash
docker tag [OPTIONS] IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]NAME[:TAG]
```

```bash
# 将镜像ubuntu:15.10标记为 runoob/ubuntu:v3 镜像
root@runoob:~# docker tag ubuntu:15.10 runoob/ubuntu:v3
```

#### build

**docker build** 命令用于使用 Dockerfile 创建镜像。


```bash
docker build [OPTIONS] PATH | URL | -
```

OPTIONS说明：
- **--build-arg=[] :**设置镜像创建时的变量；
- **--cpu-shares :**设置 cpu 使用权重；
- **--cpu-period :**限制 CPU CFS周期；
- **--cpu-quota :**限制 CPU CFS配额；
- **--cpuset-cpus :**指定使用的CPU id；
- **--cpuset-mems :**指定使用的内存 id；
- **--disable-content-trust :**忽略校验，默认开启；
- **-f :**指定要使用的Dockerfile路径；
- **--force-rm :**设置镜像过程中删除中间容器；
- **--isolation :**使用容器隔离技术；
- **--label=[] :**设置镜像使用的元数据；
- **-m :**设置内存最大值；
- **--memory-swap :**设置Swap的最大值为内存+swap，"-1"表示不限swap；
- **--no-cache :**创建镜像的过程不使用缓存；
- **--pull :**尝试去更新镜像的新版本；
- **--quiet, -q :**安静模式，成功后只输出镜像 ID；
- **--rm :**设置镜像成功后删除中间容器；
- **--shm-size :**设置/dev/shm的大小，默认值是64M；
- **--ulimit :**Ulimit配置。
- **--tag, -t:** 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。
- **--network:** 默认 default。在构建期间设置RUN指令的网络模式

```bash
# 使用当前目录的 Dockerfile 创建镜像，标签为 runoob/ubuntu:v1
docker build -t runoob/ubuntu:v1 . 
```

#### history

**docker history :** 查看指定镜像的创建历史。

```bash
docker history [OPTIONS] IMAGE
```

OPTIONS说明：
- **-H :**以可读的格式打印镜像大小和日期，默认为true；
- **--no-trunc :**显示完整的提交记录； 
- **-q :**仅列出提交记录ID。


```bash
# 查看本地镜像runoob/ubuntu:v3的创建历史
root@runoob:~# docker history runoob/ubuntu:v3
```


#### save

**docker save :** 将指定镜像保存成 tar 归档文件。

```bash
docker save [OPTIONS] IMAGE [IMAGE...]
```

OPTIONS 说明：
- **-o :**输出到的文件。


```bash
# 将镜像 runoob/ubuntu:v3 生成 my_ubuntu_v3.tar 文档
runoob@runoob:~$ docker save -o my_ubuntu_v3.tar runoob/ubuntu:v3
```

#### load

**docker load :** 导入使用 [docker save](#save) 命令导出的镜像。


```bash
docker load [OPTIONS]
```

OPTIONS 说明：
- **--input , -i :** 指定导入的文件，代替 STDIN。
- **--quiet , -q :** 精简输出信息。

```bash
# 导入镜像
$ docker load < busybox.tar.gz
```

#### import

**docker import :** 从归档文件中创建镜像。

```bash
docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]
```

OPTIONS说明：
- **-c :**应用docker 指令创建镜像； 
- **-m :**提交时的说明文字；


```bash
# 从镜像归档文件my_ubuntu_v3.tar创建镜像，命名为runoob/ubuntu:v4
runoob@runoob:~$ docker import  my_ubuntu_v3.tar runoob/ubuntu:v4  
```


----------
### 其他

#### info

docker info : 显示 Docker 系统信息，包括镜像和容器数。。

```bash
docker info [OPTIONS]
```

#### version

docker version :显示 Docker 版本信息。


```bash
docker version [OPTIONS]
```

OPTIONS说明：

- **-f :**指定返回值的模板文件。


