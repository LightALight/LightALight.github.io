---
title: 性能工具ab
date: 2017-06-15 19:23:32
tags: 性能
copyright: true
password:
toc: true
---

ab(apachebench)是apache自带的压力测试工具。ab非常实用，它不仅可以对apache服务器进行网站访问压力测试，也可以对或其它类型的服务器进行压力测试。文章介绍centos7.5环境下使用wrk进行压力测试。
<!--more-->
## Quick Guide

### 安装

```bash
# 安装
yum -y install httpd-tools

# 查看版本
ab -V
```


### 参数说明

```bash
格式：ab [options] [http://]hostname[:port]/path

# 参数说明：
-n requests     Number of requests to perform                        （要执行的请求校验次数。默认请求一次）
-c concurrency  Number of multiple requests to make                  （并发数，同一时间有多少请求发出去，默认是1）
-t timelimit    Seconds to max. wait for responses                   （校验花费的最大时间，内部设置-n 50000 次。默认不开启）
-b windowsize   Size of TCP send/receive buffer, in bytes            （发送和接收的buffer大小，单位是 bytes）
-p postfile     File containing data to POST. Remember also to set -T（包含POST数据文件）
-u putfile      File containing data to PUT. Remember also to set -T （包含PUT数据文件）
-T content-type Content-type header for POSTing, eg.                 （头信息content-type，如 -T "application/x-www-form-urlencoded" ）
                'application/x-www-form-urlencoded'
                Default is 'text/plain'
-v verbosity    How much troubleshooting info to print               （设置输出等级， 4 输出头信息，3 输出响应码(404,200) 2 输出警告和信息）
-w              Print out results in HTML tables                     （以HTML表的格式输出结果。默认时，它是白色背景的两列宽度的一张表。）
-i              Use HEAD instead of GET                              （执行HEAD请求，而不是GET）
-x attributes   String to insert as table attributes
-y attributes   String to insert as tr attributes
-z attributes   String to insert as td or th attributes
-C attribute    Add cookie, eg. -C "c1=1234,c2=2,c3=3". (repeatable) （对请求附加一个Cookie）提示：可以借助session实现原理传递 JSESSIONID参数， 实现保持会话的功能，如 -C ” c1=1234,c2=2,c3=3, JSESSIONID=FF056CD16DA9D71CB131C1D56F0319F8″ 。
-H attribute    Add Arbitrary header line, eg. 'Accept-Encoding: gzip'
                Inserted after all normal header lines. (repeatable)
-A attribute    Add Basic WWW Authentication, the attributes
                are a colon separated username and password.
-P attribute    Add Basic Proxy Authentication, the attributes        -P proxy-auth-username:password 对一个中转代理提供BASIC认证信任。用户名和密码由一个:隔开，并以base64编码形式发送。无论服务器是否需要(即, 是否发送了401认证需求代码)，此字符串都会被发送。
                are a colon separated username and password.
-X proxy:port   Proxyserver and port number to use
-V              Print version number and exit
-k              Use HTTP KeepAlive feature
-d              Do not show percentiles served table.
-S              Do not show confidence estimators and warnings.
-g filename     Output collected data to gnuplot format file.         写所有有用的信息到TSV（Tab separate values）文件，可以轻松导入Excel等里面，label在文件第一行）
-e filename     Output CSV file with percentages served               写一个逗号分隔的CSV文件，包含每个百分比(from 1% to 100%)服务器执行的时间(毫秒)，这个文件一般比'gunplot'有用
-r              Don't exit on socket receive errors.                 （在socket错误的时候不退出）
-h              Display usage information (this message)
-Z ciphersuite  Specify SSL/TLS cipher suite (See openssl ciphers)
-f protocol     Specify SSL/TLS protocol (SSL2, SSL3, TLS1, or ALL)  （指定 SSL/TLS 协议 (SSL2, SSL3, TLS1, or ALL).）
```


### 简单实例

* 并发10，请求100
    ```bash
    ab -n100 -c10 http://www.baidu.com/
    ```

* 结果以html的形式输出
    ```bash
    ab -n100 -c10 -w http://www.baidu.com/
    ```


### 测试结果说明

```bash
ab -n 100 -c 10  https://www.baidu.com/index.html

This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/
# 以上为apache的版本信息，与本次测试无关

Benchmarking www.baidu.com (be patient).....done
# 以上内容显示测试完成度，本次测试发起请求数量较少，完成较快，无中间过程显示。在请求数量很多时会分行显示当前完成数量。


Server Software:        bfe/1.0.8.14  # 被测试的服务器所用的软件信息
Server Hostname:        www.baidu.com  # 被测主机名
Server Port:            443  #被测主机的服务端口号，一般http请求的默认端口号是80，https默认使用443端口
SSL/TLS Protocol:       TLSv1.2,ECDHE-RSA-AES128-GCM-SHA256,2048,128  #加密协议

Document Path:          /index.html  # 请求的具体文件
Document Length:        227 bytes   # 请求的文件index.html大小

Concurrency Level:      10 # 并发数
Time taken for tests:   1.093 seconds  # 本次测试总共花费的时间
Complete requests:      100  # 本次测试总共发起的请求数量
Failed requests:        0  # 失败的请求数量。因网络原因或服务器性能原因，发起的请求并不一定全部成功，通过该数值和Complete requests相除可以计算请求的失败率，作为测试结果的重要参考。
Total transferred:      103314 bytes  # 总共传输的数据量，指的是ab从被测服务器接收到的总数据量，包括index.html的文本内容和请求头信息。
HTML transferred:       22700 bytes  #从服务器接收到的index.html文件的总大小，等于Document Length＊Complete requests＝227 bytes＊100＝22700 bytes
Requests per second:    91.50 [#/sec] (mean)  #平均(mean)每秒完成的请求数：QPS，这是一个平均值，等于Complete requests/Time taken for tests=100/1.093=91.50
Time per request:       109.287 [ms] (mean)  # 从用户角度看，完成一个请求所需要的时间（因用户数量不止一个，服务器完成10个请求，平均每个用户才接收到一个完整的返回，所以该值是下一项数值的10倍。）
Time per request:       10.929 [ms] (mean, across all concurrent requests)  # 服务器完成一个请求的时间。
Transfer rate:          92.32 [Kbytes/sec] received  # 网络传输速度。对于大文件的请求测试，这个值很容易成为系统瓶颈所在。要确定该值是不是瓶颈，需要了解客户端和被测服务器之间的网络情况，包括网络带宽和网卡速度等信息。

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       11   17  14.2     15     153
Processing:     4    6   2.4      5      23
Waiting:        4    6   2.1      5      23
Total:         16   23  14.6     21     158

# 这几行组成的表格主要是针对响应时间也就是第一个Time per request进行细分和统计。一个请求的响应时间可以分成网络链接（Connect），系统处理（Processing）和等待（Waiting）三个部分。表中min表示最小值;mean表示平均值;[+/-sd]表示标准差（Standard Deviation）,表示数据的离散程度，数值越大表示数据越分散，系统响应时间越不稳定;median表示中位数;max表示最大值了。

Percentage of the requests served within a certain time (ms)
  50%     21
  66%     22
  75%     23
  80%     23
  90%     25
  95%     32
  98%     52
  99%    158
 100%    158 (longest request)

# 这个表表示有百分之多少的请求都是在多少ms内完成的
```


More info: [官网](http://httpd.apache.org/docs/2.0/programs/ab.html)
