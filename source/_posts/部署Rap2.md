---
title: 部署Rap2
date: 2021-01-15 22:23:32
tags: 环境部署
copyright: true
password:
toc: true
---

Rap2是一个可视化接口管理工具,通过分析接口结构，动态生成模拟数据，校验真实接口正确性.本文章介绍如何在Centos7.5下面使用dokcer部署Rap2。
<!--more-->
## Quick Guide

![](/image/部署Rap2_001.jpg)


### 直接使用
如果想直接使用，可以点击[taobao](http://rap2.taobao.org/)通过申请一个账号后，即可在里面进行接口的编写、测试。

### 安装
#### 前置
* 安装docker
* 安装docker-compose

#### 后端部署

rap2-delos: 后端数据API服务器，基于Koa + MySQL

* 1.部署
    ```bash
    mkdir rap2
    cd rap2
    git clone https://github.com/thx/rap2-delos.git
    cd rap2-delos
    docker-compose up -d
    ```
![](/image/部署Rap2_002.png)

* 2.初始化数据库
    ```bash
    docker exec -it rap2-delos sh 
    node scripts/init
    exit
    ```
![](/image/部署Rap2_003.png)

* 3.重新启动服务
    ```bash
    docker-compose down
    docker-compose up -d
    ```
![](/image/部署Rap2_004.png)

* 4.测试
    ```bash
    curl localhost:38080
    ```
![](/image/部署Rap2_005.png)


#### 前端部署

rap2-dolores: 前端静态资源，基于React

* 1.拉取代码
    ```bash
    cd ..
    git clone https://github.com/thx/rap2-dolores.git
    cd rap2-dolores
    ```

* 2.创建Dockerfile,复制下面内容到里面
    ```bash
    vi Dockerfile
    ```

    Dockerfile中的内容为：
    ```bash
    # 拉取10.1.0版本的node镜像
    FROM node:10.1.0

    # 维护人
    MAINTAINER ryn

    # 创建工作目录
    RUN mkdir -p /home/rap2-dolores
    WORKDIR /home/rap2-dolores

    # 将代码拷贝至工作目录
    COPY . /home/rap2-dolores

    # 全局安装http-server服务器
    RUN npm install -g http-server

    # 全局安装node-sass(一定要带--unsafe-perm，否则会报错)
    RUN npm install --unsafe-perm -g node-sass

    # 安装依赖
    RUN npm install

    # 打包
    RUN npm run build
    ```

* 3.创建docker-compose,把下面内容拷贝进去
    ```bash
    vi docker-compose.yml
    ```

    docker-compose.yml中的内容为：

    ```yaml
    version: '2.2'

    services:
      delores:
        # 容器名称
        container_name: rap2-dolores
        
        # 通过Dockerfile来构建本地镜像
        build: .
        
        # 通过images来构建，这里的地址暂不适用，因为src/config中的配置需要根据自己的服务器来动态构建
        # image rynxiao/rap2-dolores-nodejs
        
        # 指定工作目录
        working_dir: /home/rap2-dolores
        
        # 指定生产环境
        environment:
          - NODE_ENV=production
          
        # 启动http-server，并映射端口到容器内部8081上
        command: /bin/sh -c 'http-server ./build -s -p 8081'
        privileged: true
        
        # expose port 38081
        ports:
          - "38081:8081"
    ```

* 4.更改src/config/config.prod.js中的配置，将接口请求地址指向你的后端服务器

    ```bash
    vi src/config/config.prod.js
    ```
    ```js
    module.exports = {
      serve: 'http://<后端服务器ip>:38080',
      keys: ['some secret hurr'],
      session: {
        key: 'koa:sess'
      }
    }
    ```

* 5.启动服务
    ```bash
    docker-compose up -d
    ```

* 6.使用浏览器访问访问http://{前端地址}:38081

![](/image/部署Rap2_006.png)


### 基本操作

* 1.注册帐号
    ![](/image/部署Rap2_007.png)

* 2.注册成功后，进去创建一个项目仓库
    ![](/image/部署Rap2_008.png)
    ![](/image/部署Rap2_009.png)

* 3.仓库建好以后，我们进入仓库，点击新建接口
    ![](/image/部署Rap2_010.png)
    ![](/image/部署Rap2_011.png)

* 4.选择新建接口编辑参数，参数语法参考[mock.js语法规范文档](https://github.com/nuysoft/Mock/wiki/Syntax-Specification)
    ![](/image/部署Rap2_012.png)
    ![](/image/部署Rap2_013.png)

* 5.点击测试
    ![](/image/部署Rap2_014.png)


More info: [Github](https://github.com/thx/rap2-delos)
