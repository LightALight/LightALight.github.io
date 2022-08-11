---
title: 部署Tomcat
date: 2015-10-26 20:04:16
tags: [环境部署,tomcat]
copyright: true
password:
toc: true
---

Tomcat 是由 Apache 开发的一个 Servlet 容器，实现了对 Servlet 和 JSP 的支持，并提供了作为Web服务器的一些特有功能。文章介绍如何在居于Centos7.5安装Tomcat。
<!--more-->
## Quick Deploy

### 部署准备
* 1.参照下表格检查环境的JDK版本是否满足(Tomcat 8.5 要求 JDK 版本为 1.7 以上)

|Servlet Spec   |JSP Spec   |EL Spec    |WebSocket Spec |JASPIC Spec    |Apache Tomcat Version  |Latest Released Version    |Supported Java Versions
|---------------|-----------|-----------|---------------|---------------|-----------------------|---------------------------|-----------------------
|4.0            |2.3        |3.0        |1.1            |1.1            |9.0.x                  |9.0.6                      |8 and later
|3.1            |2.3        |3.0        |1.1            |1.1            |8.5.x                  |8.5.29                     |7 and later
|3.1            |2.3        |3.0        |1.1            |N/A            |8.0.x (superseded)     |8.0.50 (superseded)        |7 and later
|3.0            |2.2        |2.2        |1.1            |N/A            |7.0.x                  |7.0.85                     |6 and later(7 and later for WebSocket)
|2.5            |2.1        |2.1        |N/A            |N/A            |6.0.x (archived)       |6.0.53 (archived)          |5 and later
|2.4            |2.0        |N/A        |N/A            |N/A            |5.5.x (archived)       |5.5.36 (archived)          |1.4 and later
|2.3            |1.2        |N/A        |N/A            |N/A            |4.1.x (archived)       |4.1.40 (archived)          |1.3 and later
|2.2            |1.1        |N/A        |N/A            |N/A            |3.3.x (archived)       |3.3.2 (archived)           |1.1 and later

```bash
whereis java
```

* 2.安装JDK(详细请自行查询)



### 安装和配置

* 1.下载安装包

```bash
wget http://mirrors.hust.edu.cn/apache/tomcat/tomcat-8/v8.5.37/bin/apache-tomcat-8.5.37.tar.gz
```

* 2.解压安装包

```bash
tar -xzvf apache-tomcat-8.5.37.tar.gz
```

* 3.启动 Tomcat

```bash
./apache-tomcat-8.5.37/bin/startup.sh
```

* 4.通过curl或者浏览器访问

```bash
curl http://localhost:8080 
```
![](/image/部署OpenResty_001.png)


### 重要目录说明

* bin - Tomcat 脚本存放目录（如启动、关闭脚本）。 *.sh 文件用于 Unix 系统,*.bat 文件用于 Windows 系统
* conf - Tomcat 配置文件目录
    - server.xml 配置文件中的根元素。它的属性代表了整个 servlet 容器的特性。
* logs - Tomcat 默认日志目录
* webapps - webapp 运行的目录


### web 工程发布（例如jenkin）

* 1.打包好的 war 包放在 Tomcat 安装目录下的 webapps 目录下

```bash
mv jenkins.war apache-tomcat-8.5.37/webapps/
```

* 2.启动Tomcat(Tomcat 会自动解压 webapps 目录下的 war 包)

```bash
./apache-tomcat-8.5.37/bin/startup.sh
```

* 3.通过curl或者浏览器访问

```bash
curl http://localhost:8080/jenkins
```
![](/image/部署OpenResty_002.png)

### web 项目路径结构

* webapp                         站点根目录(例如解压后的jenkins目录)
    - META-INF                   存放工程自身相关的一些信息，元文件信息，通常由开发工具，环境自动生成。
        + MANIFEST.MF            配置清单文件
    - WEB-INF                   Java web应用的安全目录。所谓安全就是客户端无法访问，只有服务端可以访问的目录
        + classes                存放程序所需要的所有 Java class 文件
            * *.class            程序需要的 class 文件
            * *.xml              程序需要的 xml 文件
        + lib                    库文件夹
            * *.jar              程序需要的 jar 包
        + web.xml                Web应用程序的部署描述文件。它是工程中最重要的配置文件，它描述了 servlet 和组成应用的其它组件，以及应用初始化参数、安全管理约束等。
    - <userdir>                  自定义的目录
    - <userfiles>                自定义的资源文件

![](/image/部署OpenResty_003.png)

More info: [Tomcat Wiki](https://wiki.apache.org/tomcat/FrontPage)
