---
title: ELK（三）Kibana
date: 2020-10-15 19:23:32
tags: [elk,kibana]
copyright: true
password:
toc: true
---

　　Kibana 是一个针对Elasticsearch的开源分析及可视化平台，用来搜索、查看交互存储在Elasticsearch索引中的数据。使用 Kibana，可以通过各种图表进行高级数据分析及展示。 
　　本文章主要介绍 Kibana 的入门知识。

<!--more-->

## Quick Guide

　　Kibana架构为Elasticsearch定制，可以将任何结构化和非结构化数据加入Elasticsearch索引。Kibana还充分利用了Elasticsearch强大的搜索和分析功能。

### 一、优点
- 整合你的数据：Kibana能够更好地处理海量数据，并据此创建柱形图、折线图、散点图、直方图、饼图和地图。
- 复杂数据分析：Kibana提升了Elasticsearch分析能力，能够更加智能地分析数据，执行数学转换并且根据要求对数据切割分块。
- 让更多团队成员受益：强大的数据库可视化接口让各业务岗位都能够从数据集合受益。
- 接口灵活，分享更容易：使用Kibana可以更加方便地创建、保存、分享数据，并将可视化数据快速交流。
- 配置简单：Kibana的配置和启用非常简单，用户体验非常友好。Kibana 4自带Web服务器，可以快速启动运行。
- 可视化多数据源： Kibana可以非常方便地把来自[Logstash](https://www.elastic.co/products/logstash)、[ES-Hadoop](https://www.elastic.co/products/hadoop)、[Beats](https://www.elastic.co/products/beats)或第三方技术的数据整合到Elasticsearch，支持的第三方技术包括[Apache Flume](http://flume.apache.org/)、[Fluentd](http://www.fluentd.org/)等。 
- 简单数据导出： Kibana可以方便地导出感兴趣的数据，与其它数据集合并融合后快速建模分析，发现新结果。 

### 二、安装部署

- 1.已经安装Elasticsearch
- 2.从[官网](https://www.elastic.co/downloads/kibana)下载解压(与ES相同的版本)

```bash
cd /hadoop/software
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.5.1-linux-x86_64.tar.gz
tar -zxvf kibana-5.5.1-linux-x86_64.tar.gz -C /hadoop/install
mv kibana-5.5.1-linux-x86_64 kibana
```

- 3.安装 x-pack

```bash
bin/kibana-plugin install x-pack
```

- 3.配置

```bash
cd /hadoop/install/kibana/
vi config/kibana.yml

添加内容：
server.host: "master"
elasticsearch.url: "http://master:9200"
kibana.index: ".kibana"
```

- 4.启动kibana

```bash
# 先启动ES，必须是在root下运行，否则会报错，启动失败
bin/kibana
```

- 5.访问：打开 http://localhost:5601 （默认的用户名：elastic，密码：changeme）

![](/image//ELK03/ELK03_001.png)

- 6.修改密码

```bash
curl -XPUT -u elastic 'localhost:9200/_xpack/security/user/kibana/_password' -d '{
  "password" : "123456"
}
```


- 7.单击侧面导航中的 Discover 进入 Kibana 的数据探索功能：

![](/image//ELK03/ELK03_002.png)

- 8.使用查询栏编写语句查询

![](/image//ELK03/ELK03_003.png)



### 三、加载自定义索引

- 1.单击 Management 选项
![](/image//ELK03/ELK03_004.png)
- 2.然后单击 Index Patterns 选项。
![](/image//ELK03/ELK03_005.png)
- 3.点击Create index pattern定义一个新的索引模式。
![](/image//ELK03/ELK03_006.png)
- 4.点击Next step
![](/image//ELK03/ELK03_007.png)
- 5.点击Create index pattern
![](/image//ELK03/ELK03_008.png)
- 6.出来如下界面，列出了所有index中的字段
![](/image//ELK03/ELK03_009.png)
- 7.接下来，我们再来使用一下kibana查看已经导入的索引数据
![](/image//ELK03/ELK03_010.png)
![](/image//ELK03/ELK03_011.png)

### 四、搜索数据

　　左上方是 填入条件过滤，右上方是数据的时间范围，左侧栏是 搜索结果的展示字段（具体参考[官方文档](https://www.elastic.co/guide/cn/kibana/current/discover.html)）

![](/image//ELK03/ELK03_012.png)


More info: [Kibana](https://www.cnblogs.com/chenqionghe/p/12503181.html?utm_source=tuicool&utm_medium=referral)

