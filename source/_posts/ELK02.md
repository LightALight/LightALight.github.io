---
title: ELK（二）Logstash
date: 2020-09-15 19:23:32
tags: [elk,logstash]
copyright: true
password:
toc: true
---

　　Logstash 是一个开源数据收集引擎，具有实时管道功能。Logstash 可以动态地将来自不同数据源的数据统一起来，并将数据标准化到你所选择的目的地。 
　　本文章主要介绍 Logstash 的入门知识。

<!--more-->

## Quick Guide

　　**Logstash**是一个开源的服务器端数据处理管道，可以同时从多个数据源获取数据，并对其进行转换，然后将其发送到你最喜欢的“存储”。（Elasticsearch）


###  流程

#### 1.输入：采集各种样式、大小和来源的数据
　　数据往往以各种各样的形式，或分散或集中地存在于很多系统中。Logstash 支持各种输入选择 ，可以在同一时间从众多常用来源捕捉事件。能够以连续的流式传输方式，轻松地从您的日志、指标、Web 应用、数据存储以及各种 AWS 服务采集数据。

![](/image/ELK02/ELK02_001.png)

#### 2.过滤器：实时解析和转换数据

　　数据从源传输到存储库的过程中，Logstash 过滤器能够解析各个事件，识别已命名的字段以构建结构，并将它们转换成通用格式，以便更轻松、更快速地分析和实现商业价值。Logstash 能够动态地转换和解析数据，不受格式或复杂度的影响：
- 利用 Grok 从非结构化数据中派生出结构
- 从 IP 地址破译出地理坐标
- 将 PII 数据匿名化，完全排除敏感字段
- 整体处理不受数据源、格式或架构的影响

![](/image/ELK02/ELK02_002.png)

#### 3.输出：选择你的存储，导出你的数据

　　尽管 Elasticsearch 是我们的首选输出方向，能够为我们的搜索和分析带来无限可能，但它并非唯一选择。
　　Logstash 提供众多输出选择，您可以将数据发送到您要指定的地方，并且能够灵活地解锁众多下游用例。

![](/image/ELK02/ELK02_003.png)

### 安装

#### 1.前置

安装 java 8 以上版本（包含）

#### 2.[官网](https://www.elastic.co/downloads/logstash)下载解压

```bash
wget https://artifacts.elastic.co/downloads/logstash/logstash-5.6.1.tar.gz -o /hadoop/software
tar -zxvf /hadoop/software/logstash-5.6.1.tar.gz -C /hadoop/install
mv /hadoop/install/logstash-5.6.1 /hadoop/install/logstash
```

#### 3.测试


- 1.简单输出到控制台

```yaml
cd /hadoop/install/logstash
bin/logstash -e 'input { stdin { } } output { stdout {} }'
```

- 2.新建配置文件：

```bash
vi logstash.conf
```
配置内容：

```bash
input { 
   file {
    type => "server"
    codec =>json
    #读取文件的位置，一定准确，否则elasticsearch读取不到
    path  =>"/logs/finance/1.log

  }
 }
 filter {
       grok {
              match => { "message" => "^%{TIMESTAMP_ISO8601}" }
       }
}
output {
  elasticsearch { 
       hosts => ["localhost:9200"]  #写入到elasticsearch中的地址信息
	   index => "trace_test_log"    #文档索引
	   }
}
```


- 3.使用配置

```bash
bin/logstash -f logstash.conf
```

- 4.访问http://localhost:9600/ 