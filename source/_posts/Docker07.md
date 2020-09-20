---
title: Docker（七）Docker Registry
date: 2018-12-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---

Docker Registry 是所有仓库（包括共有和私有）以及工作流的中央Registry。本章介绍Docker Registry的工作角色。

<!--more-->

## Quick Guide

### Docker Registry 

Docker Registry有三个角色，分别是index、registry和registry client。


- 1.Index:负责并维护有关用户帐户、镜像的校验以及公共命名空间的信息。它使用以下组件维护这些信息：
    - Web UI
    - 元数据存储
    - 认证服务
    - 符号化


- 2.Registry:是镜像和图表的仓库。然而，它没有一个本地数据库，也不提供用户的身份认证，由S3、云文件和本地文件系统提供数据库支持。此外，通过Index Auth service的Token方式进行身份认证。
    - Sponsor Registry：第三方的registry，供客户和Docker社区使用。
    - Mirror Registry：第三方的registry，只让客户使用。
    - Vendor Registry：由发布Docker镜像的供应商提供的registry。
    - Private Registry：通过设有防火墙和额外的安全层的私有实体提供的registry。

- 3.Registry Client:Docker充当registry客户端来负责维护推送和拉取的任务，以及客户端的授权。

### 工作流程详解

- 1:用户要获取并下载镜像。所涉及的步骤如下：
    - 1.用户发送请求到index来下载镜像。
    - 2.index 发出响应，返回三个相关部分信息：
       - 该镜像所处的registry
       - 该镜像包括所有层的校验
       - 以授权为目的的Token > 注意：当请求header里有X-Docker-Token时才会返回Token。而私人仓库需要基本的身份验证，对于公有仓库这一点不是强制性的。
    - 3.用户通过响应后返回的Token和registry沟通，registry全权负责镜像，它用来存储基本的镜像和继承的层。
    - 4.registry现在要与index证实该token是被授权的。
    - 5.index会发送“true” 或者 “false”给registry，由此判定是否允许用户下载所需要的镜像。



![](/image/Docker07/Docker07_001.png)



- 2:用户想要将镜像推送到registry中。其中涉及的步骤如下：
    - 1.用户发送附带证书的请求到index要求分配库名。
    - 2.在认证成功，命名空间可用之后，库名也被分配。index发出响应返回临时的token。
    - 3.镜像连带token，一起被推送到registry中。
    - 4.registry与index证实token被授权，然后在index验证之后开始读取推送流。
    - 5.该index由Docker校验的镜像更新。



![](/image/Docker07/Docker07_002.png)



- 3.用户想要从index或registry中删除镜像：
    - 1.index接收来自Docker一个删除库的信号。
    - 2.如果index对库验证成功，它将删除该库，并返回一个临时的token。
    - 3.registry现在接收到带有该token的删除信号。
    - 4.registry与index核实该token，然后删除库以及所有与其相关的信息。
    - 5.Docker现在通知有关删除的index，然后index移除库的所有记录。



![](/image/Docker07/Docker07_003.png)


- 4：用户希望在没有index的独立模式中使用registry。
    使用没有index的registry，这完全由Docker控制，它最适合于在私有网络中存储镜像。registry运行在一个特殊的模式里，此模式限制了registry与Docker index的通信。所有有关安全性和身份验证的信息需要用户自己注意。

- 5：用户想要在有index的独立模式中使用registry。
    在这种情况下，一个自定义的index会被创建在私有网络里来存储和访问镜像的问题。然而，通知Docker有关定制的index是耗时的。 Docker提供一个有趣的概念chaining registries，从而，实现负载均衡和为具体请求而指定的registry分配。在接下来的Docker教程系列中，我们将讨论如何在上述每个情景中使用Docker Registry API ，以及深入了解Docker Security。