---
title: App测试(二) adb工具的基本使用
date: 2021-07-15 19:23:32
tags: [app,adb]
copyright: true
password:
toc: true
---

adb全称Android Debug Bridge，是Android SDK中的一个工具, 使用adb可以直接操作管理Android模拟器或者真实的Andriod设备，就是起到调试桥的作用。文章介绍adb的基本使用。
<!--more-->
## Quick Guide

### adb的安装

adb工具包一般只是一个压缩文件，不需要安装，只需要解压即可。解压后有三个必须文件，adb.exe动态链接库文件、adbWinApi.dll和adbWinUsbApi.dll，解压后即可直接使用。
如图：

![](/image/App测试02/App测试02_001.png)

### adb的基本使用

进入到adb目录，cmd打开命令窗口

- 连接上设备

```bash
adb connect ip
```

注意：第一次链接失败，再连一次就成功了！

- 查看当前连接的所有设备

```bash
adb devices
```

- 推送文件到设备

```bash
adb push 电脑文件的路径 /sdcard
```

- 在设备上的文件管理器找到相关.apk文件
- 断开连接

```bash
adb disconnect
```

### 常用命令

- 获取设备列表和设备状态

```bash
adb devices
```

- 安装/卸载app

```bash
adb install 包信息

adb install -r 包信息    //覆盖安装

adb install -d 包信息    //安装的版本比手机上的版本低

adb uninstall pkname    //卸载
```

- 将PC机上的文件push到手机上

```bash
adb push 文件 /sdcard/
```

- 将手机上的文件pull到PC机上

```bash
adb pull /sdcard/50.zip（文件） D:\back（路径）

```

- 查看adb后台进程

```bash
adb shell ps | findstr adbd
```

- 获取当前界面的包名信息

```bash
adb shell dumpsys window | findstr mCurrentFocus
```

- app禁用命令、启用命令

```bash
adb shell pm disable-user 包名    # 禁用命令

adb shell pm enable 包名    # 启用命令
```

- 内存快速填充命令

```bash
# 快速填充1G内存
adb shell dd if=/dev/zero of=/sdcard/file bs=1024000 count=1024    
```

- 获取手机品牌

```bash
adb shell getprop ro.product.brand
```

- 截屏

```bash
adb shell screencap -p /sdcard/screenshot.png
```

- 重启手机

```bash
adb reboot
```

- 一般问题log的抓抓取adb LOG

```bash

# //一般问题log的抓取
adb shell -v time > D:\log.txt

# 显示问题log的抓取
adb shell dumpsys SurfaceFlinger > D:\SF.txt

# adb 查看所有进程信息
adb shell ps

# adb 查看指定关键字的进程信息 *** 为关键字 可以为包名
adb shell “ps | grep ***”

# adb 查看所有进程的 log信息
adb logcat -v process

# adb 查看指定PID的log信息
adb logcat -v process | grep ****

# 查看所有的log日志
adb logcat

# 过滤查看指定关键字的log ***为关键字
adb logcat | grep ***
```

### 抓包

#### 安装正常

1. 安装chrome 插件 Android Debug Bridge
2. 手机开启调试模式，且手机的包需要时 开发包（dev），然后usb连接手机
3. 浏览器输入 chrome://inspect ，手机进入对应h5页面，然后在浏览器就可以看到并inspect
   
![](/image/App测试02/App测试02_002.png)

#### 技巧

- [Chrome DevTools 调试技巧](https://blog.csdn.net/weixin_40398599/article/details/102818136?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=1328740.50354.16170887036072893&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)
- [最新 Chrome DevTools(v57) 使用详解](https://blog.csdn.net/weixin_33863087/article/details/89132834?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=1328740.50354.16170887036072893&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)

#### 问题

- 1.不能访问404
  - 网络问题：看能不能访问 [https://chrome-devtools-frontend.appspot.com/](https://chrome-devtools-frontend.appspot.com/)
  - 浏览器版本：被调试端版本过低（调试端 的浏览器版本 是否低于 被调试）；
