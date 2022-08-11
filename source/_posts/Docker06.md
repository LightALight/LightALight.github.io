---
title: Docker（六）Docker Swarm
date: 2018-11-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---

[Docker Swarm]( https://github.com/docker/classicswarm ) 和 Docker Compose 一样，都是 Docker 官方容器编排项目，但不同的是，Docker Compose 是一个在单个服务器或主机上创建多个容器的工具，而 Docker Swarm 则可以在多个服务器或主机上创建容器集群服务，对于微服务的部署，显然 Docker Swarm 会更加适合。  本文章介绍如何使用 Docker  Swarm 。

<!--more-->

## Quick Guide

![](/image/Docker06/Docker06_001.png)

从 Docker 1.12.0 版本开始，Docker Swarm 已经包含在 Docker 引擎中（docker swarm），并且已经内置了服务发现工具，我们就不需要像之前一样，再配置 Etcd 或者 Consul 来进行服务发现配置了。

Swarm Deamon 只是一个调度器(Scheduler)和路由器(router),自身不运行容器，只接受Docker客户端发来的请求，调度适合的节点来运行容器。意味着即使Swarm由于某些原因挂掉了，集群中的节点也会照常运行，当Swarm重新恢复运行之后，他会收集重建集群信息。

### 运行机制

 Swarm是典型的master-slave结构，通过发现服务来选举manager。manager是中心管理节点，各个node上运行agent接受manager的统一管理，集群会自动通过Raft协议分布式选举出manager节点，无需额外的发现服务支持，避免了单点的瓶颈问题，同时也内置了DNS的负载均衡和对外部负载均衡机制的集成支持。 下图是Docker Client使用Swarm对 集群(Cluster)进行调度使用。 

![](/image/Docker06/Docker06_002.png)



### 基本概念

- 1.Swarm
集群的管理和编排是使用嵌入docker引擎的SwarmKit，可以在docker初始化时启动swarm模式或者加入已存在的swarm。子命令有init, join, leave, update。（docker swarm --help查看帮助）

- 2.Node：node是加入到swarm集群中的一个docker引擎实体，可以在一台物理机上运行多个node。子命令有accept, promote, demote, inspect, update, tasks, ls, rm。（docker node --help查看帮助）
	- manager node管理节点：执行集群的管理功能，维护集群的状态，选举一个leader节点去执行调度任务。
	- worker node工作节点：接收和执行任务。参与容器集群负载调度，仅用于承载task。

- 3.Service服务：一个服务是工作节点上执行任务的定义。创建一个服务，指定了容器所使用的镜像和容器运行的命令。子命令有create, inspect, update, remove, tasks。（docker service--help查看帮助）

- 4.Task任务：一个任务包含了一个容器及其运行的命令。task是service的执行实体，task启动docker容器并在容器中执行任务。





### 工作模式

1. Node

![](/image/Docker06/Docker06_003.png)

2. Service

![](/image/Docker06/Docker06_004.png)

3. 任务与调度

![](/image/Docker06/Docker06_005.png)

4. 服务副本与全局服务

![](/image/Docker06/Docker06_006.png)



### Swarm的调度策略


Swarm在调度(scheduler)节点（leader节点）运行容器的时候，会根据指定的策略来计算最适合运行容器的节点，目前支持的策略有：spread, binpack, random.

- 1.Random
顾名思义，就是随机选择一个Node来运行容器，一般用作调试用，spread和binpack策略会根据各个节点的可用的CPU, RAM以及正在运
行的容器的数量来计算应该运行容器的节点。

- 2.Spread
在同等条件下，Spread策略会选择运行容器最少的那台节点来运行新的容器，binpack策略会选择运行容器最集中的那台机器来运行新的节点。
使用Spread策略会使得容器会均衡的分布在集群中的各个节点上运行，一旦一个节点挂掉了只会损失少部分的容器。

- 3.Binpack
Binpack策略最大化的避免容器碎片化，就是说binpack策略尽可能的把还未使用的节点留给需要更大空间的容器运行，尽可能的把容器运行在
一个节点上面。


### 使用

以下示例，均以 Docker Machine 和 virtualbox 进行介绍，确保你的主机已安装 virtualbox。

- 1.创建 swarm 集群管理节点（manager）
```bash
# 创建 docker 机器
$ docker-machine create -d virtualbox swarm-manager
```

![](/image/Docker06/Docker06_007.png)

```bash
# 初始化 swarm 集群，进行初始化的这台机器，就是集群的管理节点。
$docker-machine ssh swarm-manager
$ docker swarm init --advertise-addr 192.168.99.107 #这里的 IP 为创建机器时分配的 ip。
```

![](/image/Docker06/Docker06_008.png)

以上输出，证明已经初始化成功。需要把以下这行复制出来，在增加工作节点时会用到：

```bash
docker swarm join --token SWMTKN-1-4oogo9qziq768dma0uh3j0z0m5twlm10iynvz7ixza96k6jh9p-ajkb6w7qd06y1e33yrgko64sk 192.168.99.107:2377
```

- 2.创建 swarm 集群工作节点（worker）

	这里直接创建好俩台机器，swarm-worker1 和 swarm-worker2 。
	![](/image/Docker06/Docker06_009.png)

	分别进入两个机器里，用到上一步复制的内容,添加至上一步中创建的集群.
	```bash
	$ docker swarm join --token SWMTKN-1-4oogo9qziq768dma0uh3j0z0m5twlm10iynvz7ixza96k6jh9p-ajkb6w7qd06y1e33yrgko64sk 192.168.99.107:2377
	```

	![](/image/Docker06/Docker06_010.png)
	以上数据输出说明已经添加成功。



- 3.查看集群信息

	进入管理节点，执行：docker info 可以查看当前集群的信息。

    ```bash
    $ docker info
    ```

	![](/image/Docker06/Docker06_011.png)

	通过画红圈的地方，可以知道当前运行的集群中，有三个节点，其中有一个是管理节点。

- 4.部署服务到集群中

    **注意**：跟集群管理有关的任何操作，都是在管理节点上操作的。

    以下例子，在一个工作节点上创建一个名为 helloworld 的服务，这里是随机指派给一个工作节点：

    ```bash
    docker@swarm-manager:~$ docker service create --replicas 1 --name helloworld alpine ping docker.com
    ```

	![](/image/Docker06/Docker06_012.png)
	
- 5.查看服务部署情况

    查看 helloworld 服务运行在哪个节点上，可以看到目前是在 swarm-worker1 节点：

    ```bash
    docker@swarm-manager:~$ docker service ps helloworld
    ```
	![](/image/Docker06/Docker06_013.png)

	查看 helloworld 部署的具体信息：

    ```bash
    docker@swarm-manager:~$ docker service inspect --pretty helloworld
    ```

	![](/image/Docker06/Docker06_014.png)

- 6.扩展集群服务

	我们将上述的 helloworld 服务扩展到俩个节点。

    ```bash
    docker@swarm-manager:~$ docker service scale helloworld=2
    ```

	![](/image/Docker06/Docker06_015.png)

	可以看到已经从一个节点，扩展到两个节点。

	![](/image/Docker06/Docker06_016.png)

- 7.删除服务

    ```bash
    docker@swarm-manager:~$ docker service rm helloworld
    ```

	![](/image/Docker06/Docker06_017.png)

	查看是否已删除：

	![](/image/Docker06/Docker06_018.png)

- 8.滚动升级服务

	以下实例，我们将介绍 redis 版本如何滚动升级至更高版本。
	创建一个 3.0.6 版本的 redis。

    ```bash
    docker@swarm-manager:~$ docker service create --replicas 1 --name redis --update-delay 10s redis:3.0.6
    ```

	![](/image/Docker06/Docker06_019.png)

	滚动升级 redis

    ```bash
    docker@swarm-manager:~$ docker service update --image redis:3.0.7 redis
    ```

	![](/image/Docker06/Docker06_020.png)
	
	看图可以知道 redis 的版本已经从 3.0.6 升级到了 3.0.7，说明服务已经升级成功。

- 9.停止某个节点接收新的任务

    查看所有的节点：

    ```bash
    docker@swarm-manager:~$ docker node ls
    ```

	![](/image/Docker06/Docker06_021.png)

	可以看到目前所有的节点都是 Active, 可以接收新的任务分配。

	停止节点 swarm-worker1：

	![](/image/Docker06/Docker06_022.png)
    **注意**：swarm-worker1 状态变为 Drain。不会影响到集群的服务，只是 swarm-worker1 节点不再接收新的任务，集群的负载能力有所下降。

	可以通过以下命令重新激活节点：

    ```
    docker@swarm-manager:~$  docker node update --availability active swarm-worker1
    ```
	![](/image/Docker06/Docker06_023.png)
	

More info: [Docker Swarm](https://www.cnblogs.com/zhujingzhi/p/9792432.html)