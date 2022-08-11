---
title: Docker（三）Dockerfile
date: 2018-08-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---

Dockerfile 是记录了镜像是如何被构建出来的配置文件, 可以被 docker 直接执行以创建一个镜像。文章介绍如何编写Dockerfile。
<!--more-->

## Quick Guide


![](/image/Docker03/Docker03_001.png)

### 编写Dockerfile 构建镜像

- 1.创建文件

```bash
mkdir Dockerfile
cd Dockerfile
vi Dockerfile
```

- 2.编写镜像信息

	分为四部分：
    - 基础镜像信息
    - 维护者信息
    - 镜像操作指令
    - 容器启动时执行指令。

Dockerfile中每一个指令都会建立一层，** 最多127层镜像**， 可以用&&将各个所需命令串联起来简化为了1层。 ‘#’ 为 Dockerfile 中的注释。

```bash
# This my first nginx Dockerfile
# Version 1.0

# Base images 基于基础镜像上构建
FROM centos

#MAINTAINER 维护者信息
MAINTAINER xiaoming 

#ENV 设置环境变量
ENV PATH /usr/local/nginx/sbin:$PATH

#ADD  文件放在当前目录下，拷过去会自动解压
ADD nginx-1.8.0.tar.gz /usr/local/  
ADD epel-release-latest-7.noarch.rpm /usr/local/  

#RUN 执行以下命令 
RUN rpm -ivh /usr/local/epel-release-latest-7.noarch.rpm
RUN yum install -y wget lftp gcc gcc-c++ make openssl-devel pcre-devel pcre && yum clean all
RUN useradd -s /sbin/nologin -M www

#WORKDIR 相当于cd
WORKDIR /usr/local/nginx-1.8.0 

RUN ./configure --prefix=/usr/local/nginx --user=www --group=www --with-http_ssl_module --with-pcre && make && make install

RUN echo "daemon off;" >> /etc/nginx.conf

#EXPOSE 映射端口
EXPOSE 80

#CMD 运行以下命令
CMD ["nginx"]
```

- 3.构建镜像

```
docker build [options] PATH | URL

# [OPTIONS]
-t <指定镜像的名字>
-f <指定构建镜像的 Dockerfile 文件（Dockerfile 可不在当前路径下）>
PATH|URL # 指定构建镜像的上下文的路径，构建镜像的过程中，可以且只可以引用上下文中的任何文件 
```


```bash
docker build -t nginx:test .
```

### Dockerfile 常用命令

![](/image/Docker03/Docker03_002.png)

|指令           |说明|
|:---------------:|:-----------------------:|
|FROM           |指定所创建镜像的基础镜像|
|MAINTAINER     |指定维护者信息|
|RUN            |运行命令|
|CMD            |指定启动容器时默认执行的命令|
|LABEL          |指定生成镜像的元数据标签信息|
|EXPOSE         |声明镜像内服务所监听的端口|
|ENV            |指定环境变量|
|ADD            |赋值指定的路径下的内容到容器中的路径下，可以为URL；如果为tar文件，会自动解压到路径下|
|COPY           |赋值本地主机的路径下的内容到容器中的路径下；一般情况下推荐使用COPY而不是ADD|
|ENTRYPOINT     |指定镜像的默认入口|
|VOLUME         |创建数据挂载点|
|USER           |指定运行容器时的用户名或UID|
|WORKDIR        |配置工作目录|
|ARG            |指定镜像内使用的参数(例如版本号信息等)|
|ONBUILD        |配置当前所创建的镜像作为其他镜像的基础镜像时，所执行的创建操作的命令|
|STOPSIGNAL     |容器退出的信号|
|HEALTHCHECK    |如何进行健康检查|
|SHELL          |指定使用SHELL时的默认SHELL类型|


* 1.FROM:指定基础镜像，要在哪个镜像建立
    ```bash
    # 格式
    FROM <image> 
    FROM <image>:<tag> 
    ```
    第一条指令必须为 FROM 指令。FROM命令会指定镜像基于哪个基础镜像创建，接下来的命令也会基于这个基础镜像（CentOS和Ubuntu有些命令可是不一样的）。FROM命令可以多次使用，表示会创建多个镜像。

* 2.MAINTAINER：指定维护者信息
    ```bash
    # 格式
    MAINTAINER <name>
    ```

* 3.ARG:指定一些镜像内使用的参数(例如版本号信息等)，这些参数在执行docker build命令时才以--build-arg<varname>=<value>格式传入。
    ```bash
    # 格式
    ARG<name>[=<default value>]
    ```

* 4.RUN：在镜像中要执行的命令
    ```bash
    # 格式
    RUN <command>
    RUN ["executable", "param1", "param2"]
    ```
    前者默认将在 shell 终端中运行命令，即 /bin/bash -c ；后者则使用 exec 执行。指定使用其它终端可以通过第二种方式实现，例如 RUN [“/bin/bash”, “-c”,”echo hello”] 。
    每条RUN指令将在当前镜像的基础上执行指定命令，并提交为新的镜像。当命令较长时可以使用\换行。
    ```bash
    RUN apt-get update \
        && apt-get install -y libsnappy-dev zliblg-dev libbz2-dev \
        && rm -rf /var/cache/apt
    ```

* 5.WORKDIR：指定当前工作目录，相当于 cd
    ```bash
    # 格式
    WORKDIR /path/to/workdir
    ```
    为后续的 RUN 、 CMD 、 ENTRYPOINT 指令配置工作目录。
    可以使用多个 WORKDIR 指令，后续命令如果参数是相对路径，则会基于之前命令指定的路径。
    ```bash
    # 例如
    WORKDIR /a
    WORKDIR b
    WORKDIR c
    RUN pwd
    ```

* 6.EXPOSE：指定容器要打开的端口
    ```bash
    # 格式
    EXPOSE <port> [<port>...]
    ```
    告诉 Docker 服务端容器暴露的端口号，供互联系统使用。在启动容器时需要通过 -P，Docker 主机会自动分配一个端口转发到指定的端口。
    注意：
    该命令只是起到声明租用，并不会自动完成端口映射。
    在容器启动时需要使用-P(大写P)，Docker主机会自动分配一个宿主机未被使用的临时端口转发到指定的端口；使用-p(小写p)，则可以具体指定哪个宿主机的本地端口映射过来。


* 7.ENV：定义环境变量
    ```bash
    # 格式
    ENV <key> <value> # 指定一个环境变量，会被后续 RUN 指令使用，并在容器运行时保持。

    # 例如
    ENV PATH /usr/local/nginx/sbin:$PATH
    ```
    指令指定的环境变量在运行时可以被覆盖掉，如docker run --env <key>=<value> built_image。

* 8.COPY ：复制本地主机的 （为 Dockerfile 所在目录的相对路径）到容器中的
    ```bash
    # 格式
    COPY
    ```

* 9.ADD：相当于 COPY，但是比 COPY 功能更强大
    ```bash
    # 格式
    ADD <src> <dest>
    ```
    该命令将复制指定的 到容器中的 。 其中<src> 可以是Dockerfile所在目录的一个相对路径；也可以是一个 URL；还可以是一个 tar 文件，复制进容器会自动解压。
    <dest>可以使镜像内的绝对路径，或者相当于工作目录(WORKDIR)的相对路径，支持正则表达式。
    ```bash
    # 例如
    ADD *.c /code/
    ```

* 10.VOLUME：挂载目录
    ```bash
    # 格式
    USER daemon
    ```
    指定运行容器时的用户名或 UID，后续的 RUN 也会使用指定用户。当服务不需要管理员权限时，可以通过该命令指定运行用户。并且可以在之前创建所需要的用户，例如： RUN useradd -s /sbin/nologin -M www。

* 11.LABEL:用来生成用于生成镜像的元数据的标签信息
    ```bash
    # 格式
    LABEL <key>=<value> <key>=<value> <key>=<value> ...

    # 例如
    LABEL version="1.0"
    LABEL description="This text illustrates \ that label-values can span multiple lines."
    ```

* 12.ENTRYPOINT:指定镜像的默认入口命令，该入口命令会在启动容器时作为根命令执行，所有传入值作为该命令的参数
    ```bash
    # 格式
    ENTRYPOINT ["executable", "param1", "param2"]
    ENTRYPOINT command param1 param2 #（shell中执行）
    ```
    此时，CMD指令指定值将作为根命令的参数。
    每个Dockerfile中只能有一个ENTRYPOINT，当指定多个时，只有最后一个有效。
    在运行时可以被--entrypoint参数覆盖掉，如docker run --entrypoint。

* 13.CMD:指定启动容器时执行的命令
    ```bash
    # 格式
    CMD ["executable","param1","param2"] 使用 exec 执行，推荐方式；
    CMD command param1 param2 在 /bin/bash 中执行，提供给需要交互的应用；
    CMD ["param1","param2"] 提供给 ENTRYPOINT 的默认参数；
    ```
    每个 Dockerfile 只能有一条 CMD 命令。如果指定了多条命令，只有最后一条会被执行。如果用户启动容器时候指定了运行的命令，则会覆盖掉 CMD 指定的命令。

* 14.ONBUILD：在构建本镜像时不生效，在基于此镜像构建镜像时生效
    ```bash
    # 格式
    ONBUILD [INSTRUCTION]
    ```
    配置当所创建的镜像作为其它新创建镜像的基础镜像时，所执行的操作指令。

* 15.STOPSIGNAL:指定所创建镜像启动的容器接收退出的信号值
    ```bash
    # 例如
    STOPSIGNAL singnal
    ```

* 16.HEALTHCHECK：配置所启动容器如何进行健康检查(如何判断是否健康)，自Docker 1.12开始支持
    ```bash
    # 格式
    HEALTHCHECK [OPTIONS] CMD command # 根据所执行命令返回值是否为0判断；
    HEALTHCHECK NONE # 禁止基础镜像中的健康检查。

    # [OPTION]参数
    --inerval=DURATION  # (默认为：30s)：多久检查一次；
    --timeout=DURATION  # (默认为：30s)：每次检查等待结果的超时时间；
    --retries=N 　　     # (默认为：3)：如果失败了，重试几次才最终确定失败。
    ```

* 17.SHELL：指定其他命令使用shell时的默认shell类型（默认值为 ["bin/sh","-c"]）
    ```bash
    # 格式
    SHELL ["executable","parameters"]
    ```
    默认值为 ["bin/sh","-c"]




### 注意事项

* 对于Windows系统，建议在Dockerfile开头添加# escape=`来指定转移信息
* ENTRYPOINT 和 CMD 的区别：ENTRYPOINT 不能被执行时的参数覆盖掉，CMD 可以被覆盖掉默认的参数。ENTRYPOINT 指定了该镜像启动时的入口默认参数，CMD 则指定了容器启动时的命令。
* 调试dockerfile，使用dockerfile需要好久的时间，建议进入容器手动先执行dockerfile命令实践。
* 编写.dockerignore文件(过滤Dockerfile所在目录中的其他文件)
* 容器只运行单个应用
* 将多个RUN指令合并为一个
* 基础镜像的标签不要用latest
* 每个RUN指令后删除多余文件
* 选择合适的基础镜像(alpine版本最好)
* 设置WORKDIR和CMD
* 使用ENTRYPOINT (可选)
* 在entrypoint脚本中使用exec
* COPY与ADD优先使用前者
* 合理调整COPY与RUN的顺序
* 设置默认的环境变量，映射端口和数据卷
* 使用LABEL设置镜像元数据
* 添加HEALTHCHECK
* 最小化镜像的层数。
* 多行参数时应该分类，在每个换行符\前都增加一个空格。
* 对构建缓存要有清楚的认识


More info: [官方文档](https://docs.docker.com/engine/reference/builder/#shell)
