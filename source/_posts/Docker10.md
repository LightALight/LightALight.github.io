---
title:  Docker（十）Kubernetes
date: 2019-03-11 22:15:53
tags: [k8s,docker]
copyright: true
password:
toc: true
---

Kubernetes（k8s）是Google(基于borg)开源的容器集群管理系统，使用Docker对应用程序包装、实例化、运行，能方便地管理跨机器运行容器化的应用，自我修复机制使得容器集群总是运行在用户期望的状态。本文章介绍 Kubernetes 。
<!--more-->

## Quick Guide

Kubernetes的名字来自希腊语，意思是“舵手” 或 “领航员”。K8s是将8个字母“ubernete”替换为“8”的缩写。

- **可移植**: 支持公有云，私有云，混合云，多重云（multi-cloud）
- **可扩展**: 模块化, 插件化, 可挂载, 可组合
- **自动化**: 自动部署，自动重启，自动复制，自动伸缩/扩展




### 集群架构

![](/image/Docker10/Docker10_001.png)


#### Master

集群控制节点，master节点上运行着一组关键的进程

- Kubernetes API Server(kube-apiserver):集群控制的入口进程,提供 HTTP Rest 接口的关键服务程序(所有资源增、删、改、查等操作的唯一入口)
- Kubernetes Controller Manager(kube-controller-manager):所有资源对象的自动化控制中心
- Kubernetes Scheduler(kube-scheduler):资源调度(pod)的进程
- Etcd Server:Kubernetes 里所有资源对象的数据全部是保持在etcd中

![](/image/Docker10/Docker10_002.png)

#### Node

Node是Master管理的工作主机，可以是物理主机、VM等，运行Kubelet、kube-proxy和docker Engine

- kubelet: pod对应容器的创建、暂停等任务
- kube-proxy: k8s service 的通信与负载均衡机制的重要组件
- Docker Engine:dokcer 引擎，负责本机容器的创建与管理

![](/image/Docker10/Docker10_003.png)

#### 其他概念

- Pods：最小部署单元，可包含多个容器，是连接在一起的容器组合并共享文件卷。一个Pod中的多个容器应用通常是紧密耦合的，Pod在Node上被创建、启动或者销毁。

- Services：抽象服务出口。可以看作一组提供相同服务的Pod的对外访问接口，就像一个基础版本的负载均衡器,Service作用于哪些Pod是通过Label Selector来定义的
    - 拥有一个指定的名字（比如my-mysql-server）
    - 拥有一个虚拟IP（Cluster IP、Service IP或VIP）和端口号，销毁之前不会改变，只能内网访问
    - NodePort:每个Node的真实端口，能够访问Node的客户端就能通过这个端口访问到内部的Service了

- Namespace:命名空间将对象逻辑上分配到不同Namespace，可以是不同的项目、用户等区分管理，并设定控制策略，从而实现多租户。

- Volume ：Pod中能够被多个容器访问的共享目录，其生命周期与Pod相同跟容器无关。
    - EmptyDir，Pod分配到Node时创建的，初始内容为空，Pod从Node中移除时EmptyDir数久删    - 除。主要用于临时空间、CheckPoint临时保存目录等
    - hostPath，在Pod上挂载宿主机上的文件或目录，主要用于需要永久保存的
    - gcePersistentDisk,使用谷歌计算引擎上永久磁盘上的文件，写入数据永久保存。
    - awsElasticBlockStore，使用Amazon提供的EBS Volume
    - nfs，使用NFS(网络文件系统)提供的共享目录
    - iscsi，使用iSCSI设备
    - glusterfs，使用开源GlusterFS网络文件系统
    - rbd，使用Linux块设备共享存储
    - gitRepo，通过挂载一个空目录，从Git库clone一个> - git repository给Pod使用
    - secret，一个secret volume用于为Pod提供加密的信息
    - persistent Volume, "网络存储"，独立于“计算资源”而存在的实体资源，可以看做一个与Kubernetes无关的网盘

- Labels： Label以key/value形式附加到Pos、Service、RC、Node等上面，每个对象可以定义多个label，以提供Label Selector来选择对象， Label Selector有两种形式：
    - 基于等式，name=redis-slave选择k/v都相等的，env!=production选择k=env但是v!=production的
    - 基于集合，name [not] in (redis-master,redis-slave)，类似于SQL中in

- Replication controllers： 管理 Pods 的生命周期。它们确保指定数量的 Pods 会一直运行，还有实现资源伸缩。
    - 定义RC实现Pod的创建与副本数量的自动控制
    - RC 通过Lable Selector机制实现对副本的自动控制
    - 通过改变RC的Pod副本数量，实现Pod的扩容或缩容
    - 通过改变RC里Pod模板中的镜像版本，实现Pod的滚动更新

- Deployment: 1.2引入，为了更好地解决pod的编排问题，内部使用了Replica Set 实现；它相对于RC的最大的升级是可以随时知道当前Pod部署的进度

- Horizontal Pod Autocaler(HPA): Pod横向自动扩容，通过追踪分析RC控制的所有目标Pod的负载变化情况，确定是否需要针对性地调整目标Pod的副本数

- Annotation：与Lable类似，也使用key/value 键值对的形式定义，不同于Lable定义Kubernetes的元数据，它是用户任意定义的附加信息，以便于外部工具进行查找

### 组件

![](/image/Docker10/Docker10_004.png)

Kubernetes主要由以下几个核心组件组成：

- etcd:保存了整个集群的状态；
- apiserver:提供了资源操作的唯一入口，并提供认证、授权、访问控制、API注册和发现等机制；
- controller manager:负责维护集群的状态，比如故障检测、自动扩展、滚动更新等；
- scheduler:负责资源的调度，按照预定的调度策略将Pod调度到相应的机器上；
- kubelet:负责维护容器的生命周期，同时也负责Volume（CVI）和网络（CNI）的管理；
- Container runtime:负责镜像管理以及Pod和容器的真正运行（CRI）；
- kube-proxy:负责为Service提供cluster内部的服务发现和负载均衡；

除了核心组件，还有一些推荐的Add-ons：

- kube-dns:负责为整个集群提供DNS服务
- Ingress Controller:为服务提供外网入口
- Heapster:提供资源监控
- Dashboard:提供GUI
- Federation:提供跨可用区的集群
- 
### 分层架构

![](/image/Docker10/Docker10_005.png)

- 核心层：Kubernetes最核心的功能，对外提供API构建高层的应用，对内提供插件式应用执行环境
- 应用层：部署（无状态应用、有状态应用、批处理任务、集群应用等）和路由（服务发现、DNS解析等）
- 管理层：系统度量（如基础设施、容器和网络的度量），自动化（如自动扩展、动态Provision等）以及策略管理（RBAC、Quota、PSP、NetworkPolicy等）
- 接口层：kubectl命令行工具)、客户端SDK以及集群联邦
- 生态系统：在接口层之上的庞大容器集群管理调度的生态系统，可以划分为两个范畴
  - Kubernetes外部：日志、监控、配置管理、CI、CD、Workflow、FaaS、OTS应用、ChatOps等
  - Kubernetes内部：CRI、CNI、CVI、镜像仓库、Cloud Provider、集群自身的配置和管理等


### 使用步骤

```bash
# 创建集群
kubeadm init --apiserver-advertise-address=<master_ip> --kubernetes-version=<kube_version> --pod-network-cidr=<ip/netmasks>  # 初始化
kubeadm reset # 还原kubeadm init或join操作
kubectl join --token <node> <master_ip:master_port> # 在子节点执行,加入这个集群

# 部署应用
kubectl run <apply_name> \
      --image=<image> \
      --port=<nodeport>

# 发布应用
kubectl expose delpoyment <apply_name> --type="NodePort" --port <nodeport>

# 扩展应用
kubectl scale delpoyment/<apply_name> --replicas=2

# 更新应用
kubectl set image delpoyment/<apply_name> <apply_name>=<image>
```


### 常用命令

* 1.help：获取命令的相关帮助信息
    ```bash
    kubectl <command> --help
    ```

* 2.get：用于获取集群的一个或一些resource信息
    ```bash
    # 格式
    kubectl get [(-o|--output=)json|yaml|wide|custom-columns=...|custom-columns-file=...|go-template=...|go-template-file=...|jsonpath=...|jsonpath-file=...] (TYPE [NAME | -l label] | TYPE/NAME ...) [flags]

    # 获取pod信息
    kubectl get pod -o wide

    # 获取namespace信息
    kubectl get namespace

    # 查看rc和service列表
    kubectl get rc,service
    ```

* 3.describe：类似于get，get获得的是resource状态信息，describe获得的是resource集群相关的信息。
    ```bash
    # 获取pod信息
    kubectl describe pod

    # 获取namespace信息
    kubectl describe namespace

    # 显示Node的详细信息
    kubectl describe nodes <node-name>

    # 显示Pod的详细信息
    kubectl describe pods/<pod-name>

    # 显示由RC管理的Pod的信息
    kubectl describe pods <rc-name>
    ```

* 4.create：通过配置文件名或stdin创建集群resource
    ```bash
    # 格式
    kubectl create -f <file_name>
    kubectl create clusterrole NAME --verb=verb --resource=resource.group [--resource-name=resourcename] [--dry-run] # 创建一个ClusterRole
    kubectl create clusterrolebinding NAME --clusterrole=NAME [--user=username] [--group=groupname] [--serviceaccount=namespace:serviceaccountname] [--dry-run] # 为特定的ClusterRole创建ClusterRoleBinding
    kubectl create configmap NAME [--from-file=[key=]source] [--from-literal=key1=value1] [--dry-run] # 根据配置文件、目录或指定的literal-value创建configmap 
    kubectl create deployment NAME --image=image [--dry-run] # 创建具有指定名称的deployment 
    kubectl create namespace NAME [--dry-run] # 创建一个具有指定名称的namespace
    kubectl create poddisruptionbudget NAME --selector=SELECTOR --min-available=N [--dry-run] # 使用指定的name、selector和所需的最小pod数量，创建一个pod disruption budget
    kubectl create quota NAME [--hard=key1=value1,key2=value2] [--scopes=Scope1,Scope2] [--dry-run=bool] # 创建具有指定名称、hard限制和可选scopes的resourcequota
    kubectl create role NAME --verb=verb --resource=resource.group/subresource [--resource-name=resourcename] [--dry-run] # 使用单一规则创建Role
    kubectl create rolebinding NAME --clusterrole=NAME|--role=NAME [--user=username] [--group=groupname] [--serviceaccount=namespace:serviceaccountname] [--dry-run] # 为特定Role或ClusterRole创建RoleBinding
    kubectl create service <clusterip|externalname|loadbalancer|nodeport|account> # 使用指定的子命令创建 Service服务
    kubectl create secret <docker-registry|generic|tls> # 使用指定的子命令创建 secret

    # 根据yaml配置文件一次性创建service和rc
    kubectl create -f my-service.yaml -f my-rc.yaml
    
    # 根据<directory>目录下所有.yaml、.yml、.json文件的定义进行创建操作
    kubectl create -f <directory>
    ```

* 5.replace：对已有资源进行更新、替换
    ```bash
    # 格式
    kubectl replace -f <file_name>

    # 根据yaml配置文件更新nignx
    kubectl replace -f rc-nginx.yaml 
    ```

* 6.patch：在容器运行时，直接对容器进行修改属性
    ```bash
    # 格式
    kubectl patch (-f FILENAME | TYPE NAME) -p PATCH

    # 修改label为nginx-3
    kubectl patch pod rc-nginx-2-kpiqt -p '{"metadata":{"labels":{"app":"nginx-3"}}}' 
    ```

* 7.edit：在线编辑resource源的操作
    ```bash
    # 格式
    kubectl edit (RESOURCE/NAME | -f FILENAME)

    # 获取pod信息
    kubectl edit po rc-nginx-btv4j 
    ```

* 8.delete：删除资源对象
    ```bash
    # 格式
    kubectl delete ([-f FILENAME] | TYPE [(NAME | -l label | --all)])

    # 基于Pod.yaml定义的名称删除Pod
    kubectl delete -f pod.yaml

    # 删除所有包含某个label的Pod和service
    kubectl delete pods,services -l name=<label-name>

    # 删除所有Pod
    kubectl delete pods --all
    ```

* 9.apply：在原有resource的基础上进行更新，还会resource中添加一条注释，标记当前的apply

* 10.logs：用于显示pod运行中，容器内程序输出到标准输出的内容
    ```bash
    # 获取pod的日志
    kubectl logs <pod_name>
    ```

* 11.rolling-update:创建了一个新的RC， 然后一次更新一个pod方式逐步使用新的PodTemplate，最终实现Pod滚动更新，new-controller.json需要与之前RC在相同的namespace下
    ```bash
    # 格式
    kubectl rolling-update OLD_CONTROLLER_NAME ([NEW_CONTROLLER_NAME] --image=NEW_CONTAINER_IMAGE | -f NEW_CONTROLLER_SPEC)

    # 根据yaml模板更新rc-nginx-2
    kubectl rolling-update rc-nginx-2 -f rc-nginx.yaml 
    ```

* 12.scale:扩容或缩容 Deployment、ReplicaSet、Replication Controller或 Job 中Pod数量
    ```bash
    # 格式
    kubectl scale [--resource-version=version] [--current-replicas=count] --replicas=COUNT (-f FILENAME | TYPE NAME)

    # 设置pod的数量为4(原本数量小于4为扩容,大于为缩容)
    kubectl scale rc rc-nginx-3 —replicas=4 
    ```

* 13.exec：执行容器的命令
    ```bash
    # 执行Pod的data命令，默认是用Pod中的第一个容器执行
    kubectl exec <pod-name> data

    # 指定Pod中某个容器执行data命令
    kubectl exec <pod-name> -c <container-name> data

    # 通过bash获得Pod中某个容器的TTY，相当于登录容器
    kubectl exec -it <pod-name> -c <container-name> bash
    ```

* 14.attach:查看容器中以daemon形式运行的进程的输出
    ```bash
    # 获取pod的容器输出吸血流
    kubectl attach <pod-name> -c <containers_name>
    ```

* 15.run：创建并运行容器镜像、deployment 和job
    ```bash
    # 格式
    kubectl run NAME --image=image [--env="key=value"] [--port=port] [--replicas=replicas] [--dry-run=bool] [--overrides=inline-json] [--command] -- [COMMAND] [args...]

    # 启动nginx实例
    kubectl run nginx --image=nginx
    ```

* 16.expose：指定deployment、service、replica set、replication controller或pod ，并使用该资源的选择器作为指定端口上新服务的选择器
    ```bash
    # 格式
    kubectl expose (-f FILENAME | TYPE NAME) [--port=port] [--protocol=TCP|UDP] [--target-port=number-or-name] [--name=name] [--external-ip=external-ip-of-service] [--type=type]

    # 为RC的nginx创建service，并通过Service的80端口转发至容器的8000端口上
    kubectl expose rc nginx --port=80 --target-port=8000
    ```

* 17.annotate：更新一个或多个资源的Annotations信息
    ```bash
    # 格式
    kubectl annotate [--overwrite] (-f FILENAME | TYPE NAME) KEY_1=VAL_1 ... KEY_N=VAL_N [--resource-version=version]

    # 根据“pod.json”中的type和name更新pod的annotation
    kubectl annotate -f pod.json description='my frontend'
    ```

* 18.autoscale：使用 autoscaler 自动设置在kubernetes集群中运行的pod数量
    ```bash
    # 格式
    kubectl autoscale (-f FILENAME | TYPE NAME | TYPE/NAME) [--min=MINPODS] --max=MAXPODS [--cpu-percent=CPU] [flags]

    # 使用RC“foo”设定，使其Pod的数量介于1和5之间，CPU使用率维持在80％
    kubectl autoscale rc foo --max=5 --cpu-percent=80
    ```

* 19.convert：转换配置文件为不同的API版本，支持YAML和JSON格式
    ```bash
    # 格式
    kubectl convert -f <file_name>

    # 将“pod.yaml”转换为最新版本并打印到stdout
    kubectl convert -f pod.yaml
    ```

* 20.label：更新资源上的 label
    ```bash
    # 格式
    kubectl label [--overwrite] (-f FILENAME | TYPE NAME) KEY_1=VAL_1 ... KEY_N=VAL_N [--resource-version=version]

    # 给名为foo的Pod添加label unhealthy=true。
    kubectl label pods foo unhealthy=true
    ```

* 21.rollout：对资源进行管理
    ```bash
    # 格式
    kubectl rollout <history|pause|resume|status|undo>

    # 回滚到之前的deployment
    kubectl rollout undo deployment/abc
    ```

* 22.set：配置应用资源
    ```bash
    # 格式
    kubectl set <image|resources|selector|subject>

    # 将deployment的nginx容器cpu限制为“200m”，将内存设置为“512Mi”
    kubectl set resources deployment nginx -c=nginx --limits=cpu=200m,memory=5
    ```


More info: [交互教程](https://kubernetes.io/docs/tutorials/kubernetes-basics/)  [kubernetes](http://docs.kubernetes.org.cn/227.htm)
