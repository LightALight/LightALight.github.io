---
title: App测试(三) Monkey的基本使用
date: 2021-08-15 19:23:32
tags: [app,monkey]
copyright: true
password:
toc: true
---

Monkey 测试是通过向系统发送伪随机的用户事件流（如按键输入、触摸屏输入、手势输入等），实现对应用程序客户端的稳定性测试；
通俗来说，Monkey 测试即“猴子测试”，是指像猴子一样，不知道程序的任何用户交互方面的知识，就对界面进行无目的、乱点乱按的操作；
Monkey 测试是一种为了测试软件的稳定性、健壮性的快速有效的方法；
Monkey 程序是 Android 系统自带的，由 Java 语言写成，在 Android 文件系统中的存放路径是： /system/framework/monkey.jar；
Monkey 程序需要通过 adb 来运行。
文章介绍Monkey的基本使用。
<!--more-->
## Quick Guide

### 一、monkey启动步骤

1. 连接设备
2. adb shell
3. cd /system/bin
4. 输入monkey

### 二、关闭monkey

1. adb shell ps 查看进程
2. 查出 com.android.commands.monkey 进程ID
3. adb shell kill pid 杀死monkey进程

### 三、monkey 命令

```bash
adb shell monkey [options]  <event-count>
```

- -options 指monkey传入的参数，不指定则为无反馈启动，把事件任意发送到目标环境的全部包中
- -\<event-count> 指随机发送时间数。如输入100就执行100个随机事件。

### 四、操作事件

#### 1.触摸事件

按下抬起的操作，可通过--pct--touch 配置事件百分比（是由一组ACTION_DOWN和ACTION_UP）组成

#### 2.手势事件

指按下、移动、抬起、直线滑动的操作。通过--pct--motion配置百分比（由ACTION_DOWN和ACTION_MOVE和ACTION_UP组成）

#### 3.二指缩放事件

通过--pct--pinchzoom配置，

#### 4.轨迹事件

由一个或多个随机移动组成，通过--pct-tracball

#### 5.旋转屏幕

通过--pct-rotation配置百分比

#### 6.基本导航事件

现在基本没有

#### 7.主要导航事件

主要是中间键、back、菜单按键。通过--pct-majornav配置

#### 8.系统按键事件

如home、back、音量调节等，通过--pct-syskeys配置

#### 9.启动activity事件

手机开启一个activity。随机执行一个startactivity（）方法

#### 10.键盘事件

通过--pct-flip配置

### 五、monkey 参数

#### 1.常规参数

```bash
# 帮助类参数
monkey -h 
adb shell monkey -v <event-count>  
```

-v打印出日志。每个-v增加反馈信息级别，-v越多越详细，最多三个

#### 2.事件类参数

```bash
adb shell monkey -f /mnt/sdcard/test1  执行脚本文件

adb shell monkey -s 666 100  ;   -s可以重复执行之前的随机操作。每次随机事件默认生成一个seed

adb shell monkey --throttle 3000 5;   --throttle 每个指令之间增加间隔时间

adb shell monkey -v -v --pct-touch 100 200;   调整触摸事件百分比等
```

### 六、约束类参数

#### 1.包约束 (只访问包里的activity)

```bash
adb shell monkey -p com.tal.kaoyan 500
```

#### 2.activity约束

```bash
adb shell monkey -c Intent.CATEGORY_LAUNCHER 1000
```

### 七、调试类参数

#### 1.程序崩溃侯继续发送事件

```bash
adb shell monkey --ignore-crashes <event-count>
```

#### 2.超时错误继续发送事件

```bash
adb shell monkey --ignore-timeouts
```

#### 3.应用程序权限错误发生后继续发送事件

```bash
adb shell monkey --ignore-security-exceptions
```

### 八、案例

1. 测试是指定应用，因此需要使用-p指定被测app包名：com.tal.kaoyan
2. 这个测试的目的是希望模拟用户操作，因此需要让Monkey执行的事件尽可能地接近用户的常规操作，这样才可以最大限度地发现用户使用过程中可能出现的问题。因此需要对Monkey执行的事件百分比做一些调整:
3. 触摸事件和手势事件是用户最常见的操作，所以通过--pct-touch和--pct-motion将这两个事件的占比调整到40%与25%；目标应用包含了多个Activity，为了能覆盖大部分的Activity，所以通过--pct-appswitch将Activity切换的事件占比调整到10%；被测应用在测试中出现过不少横竖屏之间切换的问题，这个场景也必须关注，因此通过--pct-rotation把横竖屏切换事件调整到10%。
4. 使用-s参数来指定命令执行的seed值 Monkey会根据seed值来生成对应事件流，同一个seed生成的事件流是完全相同的。这里指定了seed值，是为了测试发现问题时，便于进行问题复现。
5. 使用--throttle参数来控制Monkey每个操作之间的时间间隔 指定操作之间的时间间隔，一方面是希望能更接近用户的操作场景，正常用户操作都会有一定的时间间隔；另一方面也是不希望因为过于频繁的操作而导致系统崩溃，尤其是在比较低端的手机上执行测试时。因此通过--throttle设置Monkey每个操作固定延迟0.4秒。
6. 使用--ignore-crashs和--ignore-timeouts参数使Monkey遇到意外时能继续执行 在执行Monkey测试时，会因为应用的崩溃或没有响应而意外终止，所以需要在命令中增加限制参数--ignore-crash和--ignore-timeouts，让Monkey在遇到崩溃或没有响应的时候，能在日志中记录相关信息，并继续执行后续的测试。
7. 使用-v指定log的详细级别 Monkey的日志输出有3个级别：日志的级别越高，其详细程度也越高。为了方便问题的定位，这里将日志设为 -v -v.

```bash
adb shell monkey -p com.tal.kaoyan
```

- --pct-touch 40 --pct-motion 25
- --pct-appswitch 10
- --pct-rotation 5
- -s 1666 --throttle 400
- --ignore-crashes
- --ignore-timeouts
- -v -v  200


### 九、monkey脚本稳定性测试

按照规范写好脚本，放在手机里，通过monkey -f调用脚本

#### 1.脚本api

```
LaunchActivity(pkg_name, cl_name)：启动应用的Activity。参数：包名和启动的Activity。
Tap(x, y, tapDuration)： 模拟一次手指单击事件。参数：x,y为控件坐标，tapDuration为点击的持续时间，此参数可省略。
UserWait(sleepTime)： 休眠一段时间
DispatchPress(keyName)： 按键。参数： keycode。 RotateScreen(rotationDegree, persist)： 旋转屏幕。 参数：rotationDegree为旋转角度， e.g. 1代表90度；persist表示旋转之后是否固定，0表示旋转后恢复，非0则表示固定不变。
DispatchString(input)： 输入字符串。
DispatchFlip(true/false)： 打开或者关闭软键盘。
PressAndHold(x, y, pressDuration)： 模拟长按事件。
Drag(xStart, yStart, xEnd, yEnd, stepCount)： 用于模拟一个拖拽操作。
PinchZoom(x1Start, y1Start, x1End, y1End, x2Start, y2Start, x2End, y2End, stepCount)： 模拟缩放手势。
LongPress()： 长按2秒。
DeviceWakeUp()： 唤醒屏幕。
PowerLog(power_log_type, test_case_status)： 模拟电池电量信息。
WriteLog()： 将电池信息写入sd卡。
RunCmd(cmd)： 运行shell命令。
DispatchPointer(downtime,eventTime,action,x,yxpressure,size,metastate,xPrecision,yPrecision,device,edgeFlags)： 向指定位置，发送单个手势。
DispatchPointer(downtime,eventTime,action,x,yxpressure,size,metastate,xPrecision,yPrecision,device,edgeFilags)： 发送按键消息。
LaunchInstrumentation(test_name,runner_name)： 运行一个instrumentation测试用例。
DispatchTrackball： 模拟发送轨迹球事件。
ProfileWait： 等待5秒。
StartCaptureFramerate()： 获取帧率。
EndCaptureFramerate(input)： 结束获取帧率。
```

#### 2.脚本格式

```bash
# Monkey脚本主要包含两部分，一部分是头文件信息，一部分是具体的monkey命令。
type = raw events
count = 1
speed = 1.0
# 下面为monkey命令
start data >>
# 具体的monkey脚本内容

```

#### 3.编写脚本

```bash
#头文件信息

type = raw events

count = 1

speed = 1.0

#启动测试
start data >>

LaunchActivity(com.tal.kaoyan,com.tal.kaoyan.ui.activity.SplashActivity)
UserWait(2000)

Tap(624,900,1000) #点击取消升级
UserWait(2000)

Tap(806,64,1000) #点击跳过
UserWait(2000)

Tap(217,378,1000) #点击用户名输入框
DispatchString(zxw1234)
UserWait(2000)

Tap(197,461,1000) #点击密码输入框
DispatchString(zxw123456)
UserWait(2000)

Tap(343,637,1000) #点击登录按钮
```

#### 4.执行脚本

```bash
adb push C:\Users\Shuqing\Desktop\kyb1.txt /sdcard

adb shell monkey -f /sdcard/kyb1.txt -v 1
```

#### 5.注意事项

头文件代码书写注意“=”两边预留空格，否则会出现如下报错。

### 十、日志管理

#### 1.日志保存方式

- 保存pc中

```bash
adb shell monkey -v -v 100 >d:\monkeylog.txt
```

- 保存在手机上

```bash
adb shell
monkey -v 100 >/sdcard/monkeylog.log
```

- 正常日志和error日志分开保存

```bash
adb shell monkey -v 100 1>d:\monkey.log  2>d:\error.log
```