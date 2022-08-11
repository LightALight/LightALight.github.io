---
title: 性能工具Locust
date: 2017-07-15 19:23:32
tags: 性能
copyright: true
password:
toc: true
---

Locust是一款开源的分布式负载测试工具。是用Python编写，易于使用，完全基于事件，即一个locust节点也可以在一个进程中支持数千并发用户，不使用回调，通过[gevent](http://www.gevent.org/)使用轻量级过程（即在自己的进程内运行）。本文章介绍在Windows7如何安装和使用Locust。
<!--more-->
## Quick Guide

### 安装

* 1.使用pip安装
    ```dos
    pip install  locust
    ```

* 2.验证安装
    ```dos
    locust -V
    ```


### 基本操作

* 1.创建一个demo

  ```python
  from locust import HttpLocust, TaskSet, task

  class WebsiteTasks(TaskSet): # 继承了TaskSet类，用于定义测试任务的
      def on_start(self):   # 进行初始化,只执行一次
          payload = {
              "username": "test_user",
              "password": "123456",
          }
          header = {
              "User-Agent":"Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36",
          }
          self.client.post("/login",data=payload,headers=header) # self.client属性的调用和使用方法和requests完全一致

      @task(5)    # 通过@task()装饰的方法为一个事务，方法的参数用于指定该行为的执行权重，参数越大每次被虚拟用户执行的概率越高，默认为1
      def index(self):   # 测试任务
          self.client.get("/")

      @task(1)
      def about(self):
          self.client.get("/about/")

  class WebsiteUser(HttpLocust): # 继承了HttpLocust类，为每个模拟用户的发送http请求和设置测试参数
      host     = "https://github.com/" # 被测系统的host，在终端中启动locust时没有指定--host参数时才会用到
      task_set = WebsiteTasks          # TaskSet类，该类定义用户任务信息，必填。这里就是:WebsiteTasks类名,因为该类继承TaskSet；
      min_wait = 5000  # 每个用户执行两个任务间隔时间的上下限（毫秒）,具体数值在上下限中随机取值，若不指定默认间隔时间固定为1秒
      max_wait = 15000
      weight = 10 # 同时运行多个Locust类时，用于控制不同类型的任务执行权重
  ```

* 2.执行流程图
    ![](/image/性能工具Locust_001.png)

* 3.使用下面命令启动,通过浏览器访问：http://localhost:8089(Locust启动网络监控器，默认为端口号为:8089）
    ```dos
    rem 执行性能脚本
    locust -f <性能测试脚本文件.py> --host=<被测试应用的URL地址,不填写就读取继承（HttpLocust）的类中定义的host值>
    ```
    ![](/image/性能工具Locust_002.png)
    ![](/image/性能工具Locust_003.png)

* 4.监控性能
  - Type： 请求的类型，例如GET/POST。
  - Name：请求的路径。
  - Request：当前请求的数量。
  - Fails：当前请求失败的数量。
  - Median：中间值，单位毫秒，一半的服务器响应时间低于该值，而另一半高于该值。
  - Average：平均值，单位毫秒，所有请求的平均响应时间。
  - Min：请求的最小服务器响应时间，单位毫秒。
  - Max：请求的最大服务器响应时间，单位毫秒。
  - Average Size：平均每个请求的大小，单位字节。
  - Current RPS：每秒钟请求的个数。
    ![](/image/性能工具Locust_003.png)

* 5.no-web模式运行启动
  ```dos
  locust -f <性能测试脚本文件.py>  --no-web -c<虚拟用户数>  -r<每秒启动虚拟用户数> -t <运行时间> --csv=<测试结果文件>
  ```

* 6.其他方式定义task
  ```python
  from locust import TaskSet

  def test_job1(obj):
      obj.client.get('/test1')

  def test_job2(obj):
      obj.client.get('/test2')

  class UserBehavior(TaskSet):
      tasks = {test_job1:1, test_job2:3}
      # tasks = [(test_job1,1), (test_job1,3)] # 两种方式等价
  ```


### 参数化
* 1.循环取数据，数据可重复使用
```python

from locust import TaskSet, task, HttpLocust
class UserBehavior(TaskSet):
    def on_start(self):
        self.index = 0
    @task
    def test_visit(self):
        url = self.locust.share_data[self.index]
        print('visit url: %s' % url)
        self.index = (self.index + 1) % len(self.locust.share_data)
        self.client.get(url)
class WebsiteUser(HttpLocust):
    host = 'http://debugtalk.com'
    task_set = UserBehavior
    share_data = ['url1', 'url2', 'url3', 'url4', 'url5']
    min_wait = 1000
    max_wait = 3000
```

* 2.保证并发测试数据唯一性，不循环取数据
  ```python
  from locust import TaskSet, task, HttpLocust
  import queue


  class UserBehavior(TaskSet):


      @task
      def test_register(self):
          try:
              data = self.locust.user_data_queue.get()
          except queue.Empty:
              print('account data run out, test ended')
              exit(0)
          print('register with user: {0}, pwd: {1}' .format(data['username'], data['password']))
          payload = {
              'username': data['username'],
              'password': data['password']
          }
          self.client.post('/register', data=payload)
          self.locust.user_data_queue.put_nowait(data)


  class WebsiteUser(HttpLocust):
      host = 'http://debugtalk.com'
      task_set = UserBehavior
      user_data_queue = queue.Queue()
      for index in range(100):
          data = {
              "username": "test%04d" % index,
              "password": "pwd%04d" % index,
              "email": "test%04d@debugtalk.test" % index,
              "phone": "186%08d" % index,
          }
          user_data_queue.put_nowait(data)
      min_wait = 1000
      max_wait = 3000
  ```

* 3.保证并发测试数据唯一性，循环取数据
  ```python
  from locust import TaskSet, task, HttpLocust
  import queue


  class UserBehavior(TaskSet):

      @task
      def test_register(self):
          try:
              data = self.locust.user_data_queue.get()
          except queue.Empty:
              print('account data run out, test ended')
              exit(0)
          print('register with user: {0}, pwd: {1}' .format(data['username'], data['password']))
          payload = {
              'username': data['username'],
              'password': data['password']
          }
          self.client.post('/register', data=payload)
          self.locust.user_data_queue.put_nowait(data)


  class WebsiteUser(HttpLocust):

      host = 'http://debugtalk.com'
      task_set = UserBehavior
      user_data_queue = queue.Queue()
      for index in range(100):
          data = {
              "username": "test%04d" % index,
              "password": "pwd%04d" % index,
              "email": "test%04d@debugtalk.test" % index,
              "phone": "186%08d" % index,
          }
          user_data_queue.put_nowait(data)
      min_wait = 1000
      max_wait = 3000
  ```


### 断言

python自带的断言assert失败后代码就不会向下走，且失败后不会被Locust报表统计进去。不写参数catch_response=False断言无效，将catch_response=True才生效。

```python
from locust import HttpLocust, TaskSet, task


class UserTask(TaskSet):

    @task
    def job(self):
        with self.client.get('/', catch_response = True) as response:
            if response.status_code == 200:
                response.success()
            else:
                response.failure('Failed!')


class User(HttpLocust):
    task_set = UserTask
    min_wait = 1000
    max_wait = 3000
    host = "https://www.baidu.com"
```


### 分布式压测

* 1.把主机中代码复制到多个从机中,主机负责收集测试数据，从机进行施压测试

* 2.启动主机
  ```dos
  locust -f <性能测试脚本文件.py>  --no-web -c<虚拟用户数>  -r<每秒启动虚拟用户数> -t <运行时间> --csv=<测试结果文件> --master
  ```

* 3.启动从机
  ```dos
  locust -f  <性能测试脚本文件.py> --slave --master-host=<主机ip>
  ```


More info: [官网](https://locust.io/)
