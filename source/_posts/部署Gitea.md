---
title: 部署Gitea
date: 2016-03-04 19:03:22
tags: [环境部署,git]
copyright: true
password:
toc: true
---

Gitea是一个极易安装，运行非常快速，安装和使用体验良好的自建Git服务,支持Linux、macOS和Windows以及各种架构(x86，amd64，还包括ARM和 PowerPC)。文章介绍在Centos7.5环境下搭建Gitea。
<!--more-->
## Quick Guide

### 前置
* 1.安装MySQL/Mariadb(版本大于5.5.3)
    ```bash
    # Centos系统
    yum install -y mariadb-server # 安装mariadb-server
    systemctl start mariadb.service # 启动服务
    systemctl enable mariadb.service # 添加到开机启动
    mysql # 本地登录Mariadb
    ```
    ```sql
    UPDATE mysql.user SET password = PASSWORD('123') WHERE USER = 'root'; # 修改密码
    FLUSH PRIVILEGES;
    ```

    # Ubuntu系统和Debian系统
    
    ```bash
    wget -O install.sh http://download.bt.cn/install/install-ubuntu.sh && sudo bash install.sh  
    ```
   
* 2.安装Git

    ```bash
    # CentOS系统
    yum -y install git

    # Debian和Ubuntu系统
    apt-get -y install git
    ```


### 安装

* 1.安装Gitea

    ```bash
    wget -O gitea https://dl.gitea.io/gitea/1.4.0/gitea-1.4.0-linux-amd64
    chmod +x gitea
    ./gitea web
    ```

* 2.用浏览器访问http://<server_ip>:3000进行初始配置登录

    ```bash
       sudo EXTERNAL_URL="http://<server_ip:port>" yum install -y gitlab-ee
    ```

    ![](/image/部署Gitea_001.png)
    ![](/image/部署Gitea_002.png)


### Docker方式安装

* 1.预置
    ```bash
    # 安装并启动Docker
    curl -sSL https://get.docker.com/ | sh
    service docker start

    # 安装Docker Compose
    curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    ```

* 2.创建并进入gitea目录
    ```bash
    # 创建并进入gitea目录
    mkdir gitea && cd gitea

    # 创建并编辑docker-compose.yml文件
    nano docker-compose.yml
    ```

* 3.创建并编辑docker-compose.yml文件(配置内容复制进去)
    ```bash
    nano docker-compose.yml
    ```
    ```yaml
    version: "2"

    networks:
     gitea:
       external: false

    services:
     server:
       image: gitea/gitea:latest
       environment:
        + USER_UID=1000
        + USER_GID=1000
       restart: always
       networks:
        + gitea
       volumes:
        + ./gitea:/data
       ports:
        + "3000:3000"
        + "222:22"
       depends_on:
        + db

     db:
       image: mysql:5.7
       restart: always
       environment:
        + MYSQL_ROOT_PASSWORD=gitea
        + MYSQL_USER=gitea
        + MYSQL_PASSWORD=gitea
        + MYSQL_DATABASE=gitea
       networks:
        + gitea
       volumes:
        + ./mysql:/var/lib/mysql
    ```

* 3.运行docker-compose.yml文件
    ```bash
    docker-compose up -d
    ```

* 4.用浏览器访问http://<server_ip>:3000进行初始配置登录


### 问题

* 1.访问http://<server_ip>:3000失败
    - 原因:需要关闭防火墙，或者打开对应的3000端口
        ```bash
        # CentOS 7
        systemctl stop firewalld.service
        systemctl disable firewalld.service

        # 其它系统
        iptables -I INPUT -p tcp --dport 3000 -j ACCEPT
        service iptables save                              
        service iptables restart
        ```

* 2.ERROR: Failed to Setup IP tables: Unable to enable SKIP DNAT rule
    - 原因:端口被占用重启docker服务，或者修改配置
        ```bash
        service docker restart
        ```

More info: [Github地址](https://github.com/go-gitea/gitea)
