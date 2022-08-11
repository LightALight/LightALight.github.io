---
title: 部署OpenResty
date: 2020-11-15 21:03:06
tags: [环境部署,nginx]
copyright: true
password:
toc: true
---

OpenResty是一个基于Nginx的可伸缩的Web平台，默认集成了Lua开发环境。文章介绍如何在居于Centos7.5安装OpenResty。
<!--more-->
## Quick Deploy

### 部署准备
* 1.检查依赖库(perl 5.6.1+, libreadline, libpcre, libssl, gcc, curl)

```bash
ldconfig  -v | grep -E 'readline|pcre|openssl'
yum list installed | grep -E 'perl|gcc|curl'
```

* 2.安装依赖库(也可以不检查,直接使用下面命令安装)

```bash
yum install readline-devel pcre-devel openssl-devel perl gcc curl
```


### 安装和配置

* 1.下载安装包

```bash
wget https://openresty.org/download/openresty-1.13.6.2.tar.gz
```

* 2.解压安装包

```bash
tar -xzvf openresty-1.13.6.2.tar.gz
```

* 3.编译(默认情况下程序会安装到 /usr/local/openresty 目录,你可以使用 ./configure --help 查看更多的配置选项)

```bash
cd openresty-1.13.6.2
./configure
make 
make install
```

### 重要目录说明

* nginx 
    - sbin
        + nignx 启动程序
    - logs
        + access.log 访问日志
        + error.log 错误日志
    - conf
        + nginx.con 配置文件

### 简单实例

* 1.创建日志和配置目录

```bash
mkdir  /home/test/logs/conf/
cd /home/test/
mkdir  logs/ conf/
```

* 2.打开配置文件

```bash
vi  conf/nginx.conf
```

* 3.新增配置

```lua
#启动一个进程
worker_processes  1; 
#设置错误日志目录
error_log logs/error.log;
events {
    worker_connections 1024;
}
http {
    server {
        #设置端口
        listen 9000;
        #设置访问路径
        location / {
            default_type text/html;
            #设置返回内容
            content_by_lua '
                ngx.say("<p>Hello, World!</p>")
            ';
        }
    }
}
```

* 3.启动 OpenResty (如果没有任何输出，说明启动成功，-p 指定我们的项目目录，-c 指定配置文件)

```bash
/usr/local/openresty/nginx/sbin/nginx -p /home/test/ -c /home/test/conf/nginx.conf
```

* 4.访问OpenResty(通过curl或者浏览器访问,返回 Hello World为启动成功)

```bash
curl http://localhost:9000/
```

More info: [新手上路](https://openresty.org/cn/installation.html)
