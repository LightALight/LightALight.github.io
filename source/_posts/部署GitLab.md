---
title: 部署GitLab
date: 2016-04-21 22:01:52
tags: [环境部署,git]
copyright: true
password:
toc: true
---

GitLab是利用 Ruby on Rails 一个开源的版本管理系统，实现一个自托管的Git项目仓库，可通过Web界面进行访问公开的或者私人项目,适合大规模。文章介绍在Centos7.5环境下搭建GitLab。
<!--more-->
## Quick Guide

### 前置
* 1.配置需求([官方配置](https://docs.gitlab.com/ce/install/requirements.html)推荐2C8G,硬盘至少有 5-10 GB)


* 2.系统防火墙中打开HTTP和SSH访问

    ```bash
    sudo yum install -y curl policycoreutils-python openssh-server
    sudo systemctl enable sshd
    sudo systemctl start sshd
    sudo firewall-cmd --permanent --add-service=http
    sudo systemctl reload firewalld
    ```

* 3.安装Postfix以发送通知电子邮件

    ```bash
    sudo yum install postfix
    sudo systemctl enable postfix
    sudo systemctl start postfix
    ```


### 安装

* 1.添加GitLab包存储库

    ```bash
    curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash
    ```

* 2.设置GitLab实例的URL

    ```bash
    sudo EXTERNAL_URL="http://<server_ip:port>" yum install -y gitlab-ee
    ```

* 3.启动并查看

    ```bash
    sudo gitlab-ctl reconfigure
    sudo gitlab-ctl status
    ```
    ![](/image/部署GitLab_001.png)

* 4.用浏览器访问刚才配置的gitlab中的EXTERNAL_URL

* 5.设置新密码,用root用户和新密码登录
![](/image/部署GitLab_002.png)
![](/image/部署GitLab_003.png)
![](/image/部署GitLab_004.png)


### 常用命令

```bash
sudo gitlab-ctl start # 启动
sudo gitlab-ctl stop # 停止
sudo gitlab-ctl status # 查看状态
sudo gitlab-ctl restart # 重启
sudo gitlab-ctl reconfigure # 修改后直接编译启动
sudo vim /etc/gitlab/gitlab.rb  # 修改默认的配置文件
gitlab-rake gitlab:check SANITIZE=true --trace    # 检查gitlab
sudo gitlab-ctl tail # 查看所有日志
sudo gitlab-ctl tail nginx/gitlab_access.log # 查看nginx访问日志
cat /opt/gitlab/embedded/service/gitlab-rails/VERSION # 查看gitlab版本
```


### 服务构成

![](/image/部署GitLab_005.png)

* nginx：静态Web服务器
* gitlab-shell：用于处理Git命令和修改authorized keys列表
* gitlab-workhorse:轻量级的反向代理服务器
* logrotate：日志文件管理工具
* postgresql：数据库
* redis：缓存数据库
* sidekiq：用于在后台执行队列任务（异步执行）
* unicorn：An HTTP server for Rack applications，GitLab Rails应用是托管在这个服务器上面的。


### 卸载GitLab

* 1.停止GitLab
    ```bash
    sudo gitlab-ctl stop
    ```

* 2.停止GitLab
    ```bash
    sudo rpm -e gitlab-ee
    ```

* 3.查看进程
    ```bash
    ps aux | grep gitlab|grep service
    ```

* 4.停止进程
    ```bash
    kill -9 <查看到的进程PID>
    ps aux | grep gitlab|grep service # 检查进程
    ```

* 5.删除所有包含gitlab文件
    ```bash
    find / -name gitlab | xargs rm -rf
    ```


### Docker方式安装

* 1.下拉镜像
    ```bash
    docker pull gitlab/gitlab-ce:latest
    ```

* 2.启动容器
    ```bash
    sudo docker run --detach \
    --hostname <server_ip> \
    --publish 444:443 --publish 8880:80 --publish 2222:22 \
    --name gitlab \
    --restart always \
    gitlab/gitlab-ce:latest
    ```

* 3.用浏览器访问http://<server_ip>:8880,使用root登录配置,可以参考[官方文档](https://docs.gitlab.com/omnibus/docker/)


### 问题

* 1.错误信息为:GitLab is taking too much time to respond,返回502
    - 处理步骤:
        + 1.查看日志,发现unicorn端口被占用

            ```bash
            sudo gitlab-ctl tail 
            ```
        ![](/image/部署GitLab_006.png)

        + 2.修改unicorn端口

            ```bash
            gitlab-ctl stop # 停止gitlab
            vi /etc/gitlab/gitlab.rb #
            ```
        ![](/image/部署GitLab_007.png)
        ![](/image/部署GitLab_008.png)
        ![](/image/部署GitLab_009.png)

        + 3.应用配置,检查是否生效
        ```bash
            sudo gitlab-ctl reconfigure # 应用配置
            sudo gitlab-ctl restart # 重启服务
            lsof -i:8081 # 检查是否生效
        ```


More info: [GitLab官网](https://about.gitlab.com/install/)
