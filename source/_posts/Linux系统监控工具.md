---
title: Linux系统监控工具
date: 2017-09-15 19:23:32
tags: 监控
copyright: true
password:
toc: true
---

多数 Linux 发行版都附带了监控工具。这些工具提供了获取系统活动的相关指标,可以用来查找问题的可能原因。文章介绍使用监控工具的基本命令。
<!--more-->
## Quick Guide

### 基本

#### Top – 进程活动监控命令

* 1.命令格式：
  ```bash
  top [参数]
  ```

* 2.命令功能：
  显示当前系统正在执行的进程的相关信息，包括进程ID、内存占用率、CPU占用率等

* 3.命令参数：
  ```
  -b 批处理
  -c 显示完整的治命令
  -I 忽略失效过程
  -s 保密模式
  -S 累积模式
  -i<时间> 设置间隔时间
  -u<用户名> 指定用户名
  -p<进程号> 指定进程
  -n<次数> 循环显示的次数
  ```

* 4.实例
  - 显示进程信息:top
      ```bash
      top - 10:47:44 up 91 days, 20:45,  1 user,  load average: 0.08, 0.04, 0.05
      Tasks:  85 total,   1 running,  84 sleeping,   0 stopped,   0 zombie
      %Cpu(s):  1.3 us,  2.0 sy,  0.0 ni, 62.0 id, 34.7 wa,  0.0 hi,  0.0 si,  0.0 st
      KiB Mem :  1882892 total,    70220 free,   228056 used,  1584616 buff/cache
      KiB Swap:  1049596 total,   908028 free,   141568 used.  1419140 avail Mem 

        PID USER      PR  NI    VIRT    RES    SHR S %MEM     TIME+ COMMAND                                                                                            
         27 root      20   0       0      0      0 S  0.0   3:12.62 kswapd0                                                                                            

      # 统计信息区:

      # 第一行:任务队列信息
      # 10:47:44 — 当前系统时间
      # up 91 days, 20:45 — 系统持续运行多久
      # 1 user — 当前有2个用户登录系统
      # load average: 0.08, 0.04, 0.05 — 每隔5秒钟检查一次活跃的进程数,后面的三个数分别是1分钟、5分钟、15分钟的负载情况。

      # 第二行:Tasks — 任务（进程）
      # 85 total - 系统现有进程
      # 1 running - 处于运行中的进程数
      # 84 sleeping - 处于休眠的进程数
      # 0 stopped - 处于停止的进程数
      # 0 zombie - 处于僵尸的进程数

      # 第三行:cpu状态信息
      # 1.3 us — 用户空间占用CPU的百分比
      # 2.0 sy — 内核空间占用CPU的百分比
      # 0.0 ni — 改变过优先级的进程占用CPU的百分比
      # 62.0 id — 空闲CPU百分比
      # 34.7 wa — IO等待占用CPU的百分比
      # 0.0 hi — 硬中断（Hardware IRQ）占用CPU的百分比
      # 0.0 si — 软中断（Software Interrupts）占用CPU的百分比
      # 0.0 st — 虚拟机占用百分比

      # 第四行:内存状态
      # 1882892 total — 物理内存总量
      # 70220 free — 使用中的内存总量
      # 228056 used — 空闲内存总量
      # 1584616 buff/cache — 缓存的内存量

      # 第五行:swap交换分区信息
      # 1049596 total — 交换区总量
      # 908028 free — 空闲交换区总量
      # 141568 used — 使用的交换区总量
      # 1419140 avail Mem — 可用于进程下一次分配的物理内存数量

      # 第六行:空行

      # 第七行以下:各进程（任务）的状态监控
      # PID — 进程id
      # USER — 进程所有者
      # PR — 进程优先级
      # NI — nice值。负值表示高优先级，正值表示低优先级
      # VIRT — 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
      # RES — 进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
      # SHR — 共享内存大小，单位kb
      # S — 进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程
      # %CPU — 上次更新到现在的CPU时间占用百分比
      # %MEM — 进程使用的物理内存百分比
      # TIME+ — 进程使用的CPU时间总计，单位1/100秒
      # COMMAND — 进程名称（命令名/命令行）
      ```

  - 显示完整命令:top -c
  - 以批处理模式显示程序信息:top -b
  - 以累积模式显示程序信息:top -S
  - 设置信息更新次数:top -n <更新次数>
  - 设置信息更新时间:top -d <间隔时间s>
  - 显示指定的进程信息:top -p <pid>
  - 显示指定的进程信息:top -p <pid>
  - 显示指定的进程信息:top -p <pid>

* 5.使用技巧
  - 多U多核CPU监控：在top基本视图中，按键盘数字“1”，可监控每个逻辑CPU的状况
  - 高亮显示当前运行进程：敲击键盘“b”（打开/关闭加亮效果）
  - 进程字段排序： 敲击键盘“x”（打开/关闭排序列的加亮效果）
  - 通过”shift + >”或”shift + <”可以向右或左改变排序列

* 6.交互命令
  在top 命令执行过程中可以使用的一些交互命令。这些命令都是单字母的，如果在命令行中使用了s 选项，其中一些命令可能会被屏蔽。

交互命令| 用法
-------|---------
m |是否显示内存信息
A |根据各种系统资源的利用率对进程进行排序，有助于快速识别系统中性能不佳的任务。
f或者F |进入 top 的交互式配置屏幕，用于根据特定的需求而设置 top 的显示。
o或者O |交互式地调整 top 每一列的顺序。
z |切换彩色或黑白模式
h |显示帮助画面，给出一些简短的命令总结说明
k |终止一个进程。
i |忽略闲置和僵死进程。这是一个开关式命令。
q |退出程序
r |重新安排一个进程的优先级别
S |切换到累计模式
s |改变两次刷新之间的延迟时间（单位为s），如果有小数，就换算成m s。输入0值则系统将不断刷新，默认值是5 s
l |切换显示平均负载和启动时间信息
t |切换显示进程和CPU状态信息
c |切换显示命令名称和完整命令行
M |根据驻留内存大小进行排序
P |根据CPU使用百分比大小进行排序
T |根据时间/累计时间进行排序
W |将当前设置写入~/.toprc文件中


#### VmStat - 虚拟内存统计

* 1.命令格式：
  ```bash
  vmstat [-a] [-n] [-t] [-S unit] [delay [ count]]
  vmstat [-s] [-n] [-S unit]
  vmstat [-m] [-n] [delay [ count]]
  vmstat [-d] [-n] [delay [ count]]
  vmstat [-p disk partition] [-n] [delay [ count]]
  vmstat [-f]
  vmstat [-V]
  ```

* 2.命令功能：
  用来获得有关进程、虚存、页面交换空间及 CPU活动的信息。

* 3.命令参数：
  ```bash
  -a：显示活跃和非活跃内存
  -f：显示从系统启动至今的fork数量 。
  -m：显示slabinfo
  -n：只在开始时显示一次各字段名称。
  -s：显示内存相关统计信息及多种系统活动数量。
  delay：刷新时间间隔。如果不指定，只显示一条结果。
  count：刷新次数。如果不指定刷新次数，但指定了刷新时间间隔，这时刷新次数为无穷。
  -d：显示磁盘相关统计信息。
  -p：显示指定磁盘分区统计信息
  -S：使用指定单位显示。参数有 k 、K 、m 、M ，分别代表1000、1024、1000000、1048576字节（byte）。默认单位为K（1024 bytes）
  -V：显示vmstat版本信息。
  ```

* 4.实例
  - 参数说明：vmstat
      ```bash
      procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
   r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
   2  0 141824  75964 112312 1470536    0    0    62    22    3    2  0  0 99  0  0
      ```

Procs（进程）参数| 含义| 说明
------------|------|----------
r |等待执行的任务数|展示了正在执行和等待cpu资源的任务个数。当这个值超过了cpu个数，就会出现cpu瓶颈。
b | 等待IO的进程数量

Memory(内存)参数| 含义| 说明
------------|------|----------
swpd |正在使用虚拟的内存大小，单位k|
free | 空闲内存大小
buff | 已用的buff大小，对块设备的读写进行缓冲
cache | 已用的cache大小，文件系统的cache
inact | 非活跃内存大小，即被标明可回收的内存，区别于free和active
active |活跃的内存大小

Swap参数| 含义| 说明
------------|------|----------
si |每秒从交换区写入内存的大小（单位：kb/s）
so | 每秒从内存写到交换区的大小

IO参数| 含义| 说明
------------|------|----------
bi |每秒读取的块数（读磁盘）
bo | 每秒写入的块数（写磁盘）

system参数| 含义| 说明
------------|------|----------
in |每秒中断数，包括时钟中断|值越大，会看到由内核消耗的cpu时间会越多
cs |每秒上下文切换数|这两个值越大，会看到由内核消耗的cpu时间会越多

CPU（以百分比表示）参数| 含义| 说明
------------|------|----------
Us |用户进程执行消耗cpu时间(user time)|us的值比较高时，说明用户进程消耗的cpu时间多，但是如果长期超过50%的使用，那么我们就该考虑优化程序算法或其他措施了
Sy |系统进程消耗cpu时间(system time)|sys的值过高时，说明系统内核消耗的cpu资源多，这个不是良性的表现，我们应该检查原因。
Id |空闲时间(包括IO等待时间)
wa |等待IO时间|Wa过高时，说明io等待比较严重，这可能是由于磁盘大量随机访问造成的，也有可能是磁盘的带宽出现瓶颈。

  - 显示活跃和非活跃内存：vmstat –a
  - 查看内存使用的详细信息：vmstat -s
  - 查看磁盘的读/写：vmstat -d


#### Lsof - 列出打开的文件

* 1.命令格式：
  ```bash
  lsof [选项] [绝对路径的文件名]
  ```

* 2.命令功能：
  用于以列表的形式显示所有打开的文件和进程。打开的文件包括磁盘文件、网络套接字、管道、设备和进程

* 3.命令参数：
  ```bash
  -a  将结果进行“与”运算（而不是“或”运算）
  -l  在输出显示用户 id 而不是用户名
  -t  仅获取进程ID
  -i  显示所有连接 
  -h  获取lsof使用帮助
  -u  显示指定用户打开了什么 
  -U  获取 UNIX 套接口地址
  -p  查看指定进程ID已打开的内容
  -F  格式化输出结果，用于其他命令。可以通过多种方式格式化，如-F pcfn（用户进程ID、命令名、文件描述符、文件名，并以空终止）
  ```

* 4.实例
  - 列出活跃进程的所有打开文件:lsof
    ```bash
    COMMAND  PID   USER  FD   TYPE DEVICE SIZE/OFF   NODE NAME
    httpd   6279   root txt    REG    8,2   344112 415135 /usr/sbin/httpd

    # COMMAND - 进程名称
    # PID - 进程标识符
    # USER: - 进程所有者
    # FD - 文件描述符，应用程序通过文件描述符识别到该文件。如cwd、txt等
    # TYPE - 文件类型，REG、DIR、CHR、BLK、UNIX、FIFO、IPV4
    # DEVICE: - 指定磁盘名称
    # SIZE - 文件大小
    # NODE - 索引节点（文件在磁盘上的标识）
    # NAME - 打开文件的确切名称
    ```

  - 获取网络信息:
    + 显示所有连接:lsof -i
    + 仅获取 IPv6 流量:lsof -i 6
    + 仅显示TCP连接:lsof -iTCP
    + 显示指定到指定主机的连接:lsof -i@<host_ip>
    + 显示基于主机与端口的连接:lsof -i@<host_ip:port>
    + 找出监听端口:lsof -i -sTCP:LISTEN
    + 找出已建立的连接:lsof -i -sTCP:ESTABLISHED
    + 显示某个端口范围的打开的连接:lsof -i@<host>:<port1>=<port2>

  - 获取用户信息
    + 显示指定用户打开了什么：lsof -u <username>
    + 显示除指定用户以外的其他所有用户所做的事情:lsof -u ^<username>
    + 杀死指定用户所做的一切事情:kill -9 'lsof -t -u <username>'
    + 查看指定的命令正在使用的文件和网络连接:lsof -c <yourcommand>
    + 查看指定进程ID已打开的内容:lsof -p <pid>


#### Tcpdump - 网络分组分析器

* 1.命令格式：
  ```bash
　　tcpdump [ -adeflnNOpqStvx ] [ -c 数量 ] [ -F 文件名 ]
　　　　　　　　[ -i 网络接口 ] [ -r 文件名] [ -s snaplen ]　　
　　　　　　　　[ -T 类型 ] [ -w 文件名 ] [表达式 ]
  ```

* 2.命令功能：
  最广泛使用的网络包分析器或者包监控程序之一，它用于捕捉或者过滤网络上指定接口上接收或者传输的TCP/IP包。它还有一个选项用于把捕捉到的包保存到文件里，以便以后进行分析。

* 3.命令参数：
    ```bash
    -A 以ASCII格式打印出所有分组，并将链路层的头最小化。 
    -c 在收到指定的数量的分组后，tcpdump就会停止。 
    -C 在将一个原始分组写入文件之前，检查文件当前的大小是否超过了参数file_size 中指定的大小。如果超过了指定大小，则关闭当前文件，然后在打开一个新的文件。参数 file_size 的单位是兆字节（是1,000,000字节，而不是1,048,576字节）。 
    -d 将匹配信息包的代码以人们能够理解的汇编格式给出。 
    -dd 将匹配信息包的代码以C语言程序段的格式给出。 
    -ddd 将匹配信息包的代码以十进制的形式给出。 
    -D 打印出系统中所有可以用tcpdump截包的网络接口。 
    -e 在输出行打印出数据链路层的头部信息。 
    -E 用spi@ipaddr algo:secret解密那些以addr作为地址，并且包含了安全参数索引值spi的IPsec ESP分组。 
    -f 将外部的Internet地址以数字的形式打印出来。 
    -F 从指定的文件中读取表达式，忽略命令行中给出的表达式。 
    -i 指定监听的网络接口。 
    -l 使标准输出变为缓冲行形式，可以把数据导出到文件。 
    -L 列出网络接口的已知数据链路。 
    -m 从文件module中导入SMI MIB模块定义。该参数可以被使用多次，以导入多个MIB模块。 
    -M 如果tcp报文中存在TCP-MD5选项，则需要用secret作为共享的验证码用于验证TCP-MD5选选项摘要（详情可参考RFC 2385）。 
    -b 在数据-链路层上选择协议，包括ip、arp、rarp、ipx都是这一层的。 
    -n 不把网络地址转换成名字。 
    -nn 不进行端口名称的转换。 
    -N 不输出主机名中的域名部分。例如，‘nic.ddn.mil‘只输出’nic‘。 
    -t 在输出的每一行不打印时间戳。 
    -O 不运行分组分组匹配（packet-matching）代码优化程序。 
    -P 不将网络接口设置成混杂模式。 
    -q 快速输出。只输出较少的协议信息。 
    -r 从指定的文件中读取包(这些包一般通过-w选项产生)。 
    -S 将tcp的序列号以绝对值形式输出，而不是相对值。 
    -s 从每个分组中读取最开始的snaplen个字节，而不是默认的68个字节。 
    -T 将监听到的包直接解释为指定的类型的报文，常见的类型有rpc远程过程调用）和snmp（简单网络管理协议；）。 
    -t 不在每一行中输出时间戳。 
    -tt 在每一行中输出非格式化的时间戳。 
    -ttt 输出本行和前面一行之间的时间差。 
    -tttt 在每一行中输出由date处理的默认格式的时间戳。 
    -u 输出未解码的NFS句柄。 
    -v 输出一个稍微详细的信息，例如在ip包中可以包括ttl和服务类型的信息。 
    -vv 输出详细的报文信息。 
    -w 直接将分组写入文件中，而不是不分析并打印出来。
    ```

* 4.实例
  - 监视第一个网络接口上所有流过的数据包:tcpdump
  - 监视指定主机的数据包:tcpdump host <host_ip>
  - 监视指定网络接口的数据包:tcpdump -i <网卡>
  - 监视主机hostname发送的所有数据:tcpdump -i <网卡> src host <hostname>
  - 监视指定主机和端口的数据包:tcpdump port <port> and host <host_ip>


#### Netstat - 网络统计
* 1.命令格式：
  ```bash
  netstat [参数]
  ```

* 2.命令功能：
  用于监视传入和传出网络数据包统计信息以及接口统计信息。

* 3.命令参数：
    ```bash
    -a (all)显示所有选项，netstat默认不显示LISTEN相关
    -t (tcp)仅显示tcp相关选项
    -u (udp)仅显示udp相关选项
    -n 拒绝显示别名，能显示数字的全部转化成数字。(重要)
    -l 仅列出有在 Listen (监听) 的服務状态

    -p 显示建立相关链接的程序名(macOS中表示协议 -p protocol)
    -r 显示路由信息，路由表
    -e 显示扩展信息，例如uid等
    -s 按各个协议进行统计 (重要)
    -c 每隔一个固定时间，执行该netstat命令。
    ```

* 4.实例
  - netstat
    ```bash
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 VM_0_4_centos:51354     169.254.0.55:lsi-bobcat ESTABLISHED

    # 第一行 
    # Ative Internet connections - 有源TCP连接

    # 第二行 
    # Proto - 协议
    # Recv-Q - 接收队列
    # Send-Q - 发送队列
    # Local Address - 本机的地址与端口
    # Foreign Address - 外部的地址与端口
    # State - 套接口当前的状态：LISTENING，ESTABLISHED，TIME_WAIT

    Active UNIX domain sockets (w/o servers)
    Proto RefCnt Flags       Type       State         I-Node   Path
    unix  3      [ ]         STREAM     CONNECTED     12869199 /usr/local/yd.socket.client

    # 第一行
    # Active UNIX domain sockets - 有源Unix域套接

    # 第二行
    # Proto - 显示连接使用的协议
    # RefCnt - 表示连接到本套接口上的进程数量
    # Types - 套接口的类型
    # State - 套接口当前的状态
    # I-Node - 索引节点
    # Path - 连接到套接口的其它进程使用的路径名
    ```
 
  - 列出所有端口
    ```bash
    列出所有端口:     netstat -a
    列出所有tcp端口:  netstat -at
    列出所有udp端口:  netstat -au
    ```

  - 列出所有处于监听状态的 Sockets
    ```bash
    只显示监听端口:          netstat -l
    只列出所有监听tcp端口:   netstat -lt
    只列出所有监听udp端口:   netstat -lu
    只列出所有监听UNIX端口:  netstat -lx
    ```

  - 显示每个协议的统计信息
    ```bash
    显示所有端口的统计信息     netstat -s
    显示TCP或UDP端口的统计信息 netstat -st 或 -su
    ```

  - 显示 PID 和进程名称:netstat -p
  - 不显示主机，端口和用户名:netstat -an
  - 持续输出 netstat 信息：netstat -t -c 2
  - 显示核心路由信息：netstat -rn
  - 找出程序运行的端口：netstat -apn
  - 显示网络接口列表：netstat -ie


### 其他工具

#### Htop - Linux进程监控

* 1.命令格式：
  ```bash
  htop [参数]
  ```

* 2.命令功能：
  强化版本的top

* 3.命令参数：
  ```bash
  -s 选项 : 按指定的列排序
  -u 选项 : 显示指定的用户的进程信息列表。
  -d 选项 : 设置刷新的延迟时间。例如 htop -d 100 命令会使输出在1秒后才会刷新（参数 -d 的单位是10微秒）。
  ```

* 4.实例
  - 显示进程信息：htop

    ![](/image/Linux系统监控工具_001.png) 

  - 按 PID 列的大小排序来显示:htop -s <pid>
  - 显示指定的用户的进程信息列表:htop -u <user_name>

* 5.交互命令

交互命令|交互命令|作用
------|---------|------------
h, ?  | F1  | 查看htop使用说明
S | F2  | htop 设定
/ | F3  | 搜索进程
\ | F4  | 增量进程过滤器
t | F5  | 显示树形结构
<, >  | F6  | 选择排序方式
[ | F7  | 可减少nice值可以提高对应进程的优先级
] | F8  | 可增加nice值，降低对应进程的优先级
k | F9  | 可对进程传递信号
q | F10 | 结束htop
u | 只显示一个给定的用户的过程   
U | 取消标记所有的进程   
H | 显示或隐藏用户线程   
K | 显示或隐藏内核线程   
F | 跟踪进程    
P | 按CPU 使用排序   
M | 按内存使用排序   
T   | 按Time+ 使用排序   
l | 显示进程打开的文件   
I | 倒转排序顺序    
s | 选择某进程，按s:用strace追踪进程的系统调用   


#### Sar - 系统活动情况报告

* 1.命令格式：
  ```bash
  sar [options] [-A] [-o file] t [n]

  # t为采样间隔，n为采样次数，默认值是1；
  # -o file表示将命令结果以二进制格式存放在文件中，file 是文件名。
  ```

* 2.命令功能：
  可以从多方面对系统的活动进行报告，包括：文件的读写情况、 系统调用的使用情况、磁盘I/O、CPU效率、内存使用状况、进程活动及IPC有关的活动等。本文主要以CentOS 6.3 x64系统为例，介绍sar命令

* 3.命令参数：
  ```bash
  -A - 所有报告的总和
  -u - 输出CPU使用情况的统计信息
  -v - 输出inode、文件和其他内核表的统计信息
  -d - 输出每一个块设备的活动信息
  -r - 输出内存和交换空间的统计信息
  -b - 显示I/O和传送速率的统计信息
  -a - 文件读写情况
  -c - 输出进程统计信息，每秒创建的进程数
  -R - 输出内存页面的统计信息
  -y - 终端设备活动情况
  -w - 输出系统交换活动信息
  ```

* 4.实例
  - 查看内存使用情况：sar -r
  - 查看内存页面交换发生状况：sar -W
  - 查看带宽信息：sar -n DEV


#### IPTraf - 实时IP局域网监控

* 1.命令格式：
  ```bash
  iptraf-ng [options]
  ```

  ![](/image/Linux系统监控工具_002.png)

* 2.命令功能：
  收集TCP，UDP，IP，ICMP，非IP，IP校验和错误，接口活动等通用和详细的接口统计信息。
