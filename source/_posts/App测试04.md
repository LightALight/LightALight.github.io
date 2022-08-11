---
title: App测试(四) Android Studio 连接手机进行调试
date: 2021-09-15 19:23:32
tags: [app,AndroidStudio]
copyright: true
password:
toc: true
---

Android Studio 是谷歌推出的一个Android集成开发工具，基于IntelliJ IDEA. 类似 Eclipse ADT，Android Studio 提供了集成的 Android 开发工具用于开发和调试。
文章介绍Android Studio的基本使用。
<!--more-->
## Quick Guide

### 配置

#### 创建第一个项目

- 进入AndroidStudio官网
- 点击Download进行下载

![](/image/App测试04/App测试04_001.png)

- 创建第一个项目
如果用kotlin 开发就选择【Empty Compose Activity】

![](/image/App测试04/App测试04_002.png)

![](/image/App测试04/App测试04_003.png)

- 【tools】->【SDK Manager】->【SDK Tools】 下载Android Emulator 和Android SDK Platform-Tools

![](/image/App测试04/App测试04_004.png)

- 可以先试试AS自带的模拟器

![](/image/App测试04/App测试04_005.png)

- 点击create device

![](/image/App测试04/App测试04_006.png)

- 选择一种型号的设备下载

![](/image/App测试04/App测试04_007.png)

- 然后运行项目就可以看到效果啦

![](/image/App测试04/App测试04_008.png)

#### 连接手机进行调试

##### ADB环境配置

- 查看自己Android Studio配置的sdk路径【tools】->【SDK Manager】比如我的路径是C:\Users\Admin\AppData\Local\Android\Sdk

![](/image/App测试04/App测试04_009.png)

- 配置环境变量：右键【我的电脑】->【高级系统设置】->【环境变量】，新建变量【Android_Home】

![](/image/App测试04/App测试04_010.png)

- 然后在Path变量中，新增加一项%Android_Home%(即为相对路径)：

![](/image/App测试04/App测试04_011.png)

- 打开cmd窗口，输入adb, 出现如下图就说明安装好啦

![](/image/App测试04/App测试04_012.png)

##### 配置USB Driver

- 下载Google USB Driver【tools】->【SDK Manager】->【SDK Tools】

![](/image/App测试04/App测试04_013.png)

- 将手机用USB线连接到电脑，打开设备管理器，找到你的手机

![](/image/App测试04/App测试04_014.png)

- 右键点击你的手机名称，选择【更新驱动设备】

![](/image/App测试04/App测试04_015.png)

- 然后再选择【浏览我的电脑以查找驱动程序】

![](/image/App测试04/App测试04_016.png)

- 找到usb_driver的安装路径(默认情况在SDK文件路径下的extras\google\usb_driver),最后点击下一页完成更新就好啦

![](/image/App测试04/App测试04_017.png)

- 打开手机的开发者模式（不同手机不一样，自行百度，这里附上华为nova系列）
  - 安卓系统的参考这篇文章：[https://www.iefans.net/info/v944581.html](https://www.iefans.net/info/v944581.html)
  - 鸿蒙系统:【设置】-> 【系统和更新】->【开发人员选项】->【USB调试】,选择允许USB调试

  ![](/image/App测试04/App测试04_018.png)


- 连接手机调试（USB线）,显示手机设备

![](/image/App测试04/App测试04_019.png)

- 然后选择手机，点击运行，就可以在手机上调试

![](/image/App测试04/App测试04_020.png)

![](/image/App测试04/App测试04_021.png)

### 功能

#### 查看性能

需要app开启debug模式

- 根据以下操作步骤选择对应链接的手机，并且手机上启动APP

![](/image/App测试04/App测试04_022.png)

- 此时进行app操作即可查看以下信息

![](/image/App测试04/App测试04_023.png)

- 在页面内点击任意一个位置 进入到具体信息页面

![](/image/App测试04/App测试04_024.png)

#### 查看日志

需要app开启debug模式

![](/image/App测试04/App测试04_025.png)

![](/image/App测试04/App测试04_026.png)

#### 截图

![](/image/App测试04/App测试04_027.png)

#### 设置无线连接

1. 手机和电脑连入同一个无线网络
2. 手机连接电脑，在命令行输入adb tcpip 5555
3. 断开连接线，命令行输入adb connect 10.3.6.59(手机的IP地址)
4. 提示连接成功后，可以进行无线调试了

### 问题

#### Failed to find Build Tools revision 30.0.3

取消然后再选中Show package detail，然后下载30.0.3
![](/image/App测试04/App测试04_028.png)