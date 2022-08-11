---
title: Docker（八）Docker API
date: 2019-01-16 21:32:11
tags: docker
copyright: true
password:
toc: true
---


Docker 本身提供了强大的API功能，我们可以通过访问Docker API来对Docker服务进行管理。
在本章介绍如何使用Docker API。


<!--more-->

## Quick Guide

### Docker API

Docker提供了很多的API以便用户使用。这些API包含四个方面：
- Docker Registry API：提供了与存储Docker镜像的Docker Registry集成的功能。
- Docker Hub API：：提供了与Docker HUB集成的功能
- Docker OAuth API: 提供了与OAuth的认证授权的功能
- Docker Remote API：：提供与Docker守护进程进行集成的功能


#### Docker Registry API

| 用途                           | 方法   | url                                                   | 样例                                                         |
| --------- | ------ | ------------------------ | ------------------------------------------------------------ |
| 取出镜像层    | GET    | /v1/images/(image_id)/layer  | ![](/image/Docker08/Docker08_001.jpg) |
| 插入镜像层                     | PUT    | /v1/images/(image_id)/layer                           |                                                      ![](/image/Docker08/Docker08_002.jpg)        |
| 检索镜像                       | GET    | /v1/images/(image_id)/json                            |                                                              |
| 检索根镜像                     | GET    | /v1/images/(image_id)/ancestry                        |                                                              |
| 获取库里所有的标签或者指定标签 | GET    | /v1/repositories/(namespace)/(repository)/tags        | ![](/image/Docker08/Docker08_003.jpg) |
| 获取库里所有的标签或者指定标签 | GET    | /v1/repositories/(namespace)/(repository)/tags/(tag*) | ![](/image/Docker08/Docker08_004.jpg) |
| 删除标签                       | DELETE | /v1/repositories/(namespace)/(repository)/tags/(tag*) | ![](/image/Docker08/Docker08_005.jpg) |
| registry状态检查               | GET    | /v1/_ping                                             | ![](/image/Docker08/Docker08_006.jpg) |
| 创建镜像                       | POST   | /images/create                                        | ![](/image/Docker08/Docker08_007.jpg) |
| 利用容器创建镜像               | POST   | /commit                                               | ![](/image/Docker08/Docker08_008.jpg) |
| 获取镜像清单                   | GET    | /images/json                                          | ![](/image/Docker08/Docker08_009.jpg) |
| 导入指定的路径文件 | POST | /images/(name)/insert | ![](/image/Docker08/Docker08_010.jpg) |
| 删除镜像 | DELETE | /images/(name) | ![](/image/Docker08/Docker08_011.jpg) |
| 推送镜像到Registry | POST | /images/(name)/push | ![](/image/Docker08/Docker08_012.jpg) |
| Tag镜像 | POST | /images/(name)/tag | ![](/image/Docker08/Docker08_013.jpg) |
| 搜索镜像 | GET | /images/search | ![](/image/Docker08/Docker08_014.jpg) |
| 查看镜像历史 | GET | /images/(name)/history | ![](/image/Docker08/Docker08_015.jpg) |
| 构建镜像 | POST | /build | ![](/image/Docker08/Docker08_016.jpg) |


#### Docker Hub API

| 用途                           | 方法   | url                                                   | 样例                                                         |
| --------- | ------ | ------------------------ | ------------------------------------------------------------ |
| **创建一个新的仓库** | PUT | /v1/repositories/(repo_name)/ |  |
| **删除已经存在的仓库** | DELETE | /v1/repositories/(repo_name)/ |  |
| **更新仓库镜像** | PUT | /v1/repositories/(repo_name)/images |  |
| **从仓库中获取镜像** | GET | /v1/repositories/(repo_name)/images |  |
| **授权** | PUT | /v1/repositories/(repo_name)/auth |  |
| **创建用户仓库** | PUT | /v1/repositories/(namespace)/(repo_name)/ | ![](/image/Docker08/Docker08_017.jpg) |
| **删除用户仓库** | DELETE | /v1/repositories/(namespace)/(repo_name)/ | ![](/image/Docker08/Docker08_018.jpg) |
| **更新用户仓库镜像** | PUT | /v1/repositories/(namespace)/(repo_name)/images | ![](/image/Docker08/Docker08_019.jpg) |
| **从仓库中下载镜像** | GET | /v1/repositories/(namespace)/(repo_name)/images | ![](/image/Docker08/Docker08_020.jpg) |
| **验证用户登录** | GET | /v1/users | ![](/image/Docker08/Docker08_021.jpg) |
| **添加新用户** | POST | /v1/users |  |
| **更新用户信息** | PUT | /v1/users/(username)/ |  |


#### Docker Remote API


| 用途                           | 方法   | url                                                   | 样例                                                         |
| --------- | ------ | ------------------------ | ------------------------------------------------------------ |
| **容器列表** | GET    | /containers/json | ![](/image/Docker08/Docker08_022.jpg) |
| **创建新容器** | POST | /containers/create | ![](/image/Docker08/Docker08_023.jpg) |
| **监控容器** | GET | /containers/(id)/json | ![](/image/Docker08/Docker08_024.jpg) |
| **进程列表** | GET | /containers/(id)/top | ![](/image/Docker08/Docker08_025.jpg) |
| **容器日志** | GET | /containers/(id)/logs | ![](/image/Docker08/Docker08_026.jpg) |
| **导出容器** | GET | /containers/(id)/export | ![](/image/Docker08/Docker08_027.jpg) |
| **启动容器** | POST | /containers/(id)/start | ![](/image/Docker08/Docker08_028.jpg) |
| **停止容器** | POST | /containers/(id)/stop | ![](/image/Docker08/Docker08_029.jpg) |
| **重启容器** | POST | /containers/(id)/restart | ![](/image/Docker08/Docker08_030.jpg) |
| **终止容器** | POST | /containers/(id)/kill | ![](/image/Docker08/Docker08_031.jpg) |


### 注意事项

- 当Docker允许与访客容器目录共享而不限制其访问权限时，Docker Daemon的控制权应该只给授权用户。
- REST API支持Unix sockets，从而防止了cross-site-scripting攻击。
- REST API的HTTP接口应该在可信网络或者VPN下使用。
- 在服务器上单独运行Docker时，需要与其它服务隔离。
- 容器以非特权用户运行。
- Apparmor、SELinux、GRSEC解决方案，可用于额外的安全层。
- 可以使用其它容器系统的安全功能。



More info:[Docker API](https://docs.docker.com/engine/api/v1.37/#)