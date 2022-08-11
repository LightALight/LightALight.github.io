---
title: 性能工具wrk
date: 2017-08-15 19:23:32
tags: 性能
copyright: true
password:
toc: true
---

wrk是一款开源的性能测试工具,支持使用lua脚本,底层封装了epoll(linux)和kqueue(bsd)。文章介绍使用wrk进行压力测试。
<!--more-->
## Quick Guide

### 安装

* Unbuntu/Debian下的安装
    ```bash
    Unbuntu/Debian下的安装
    sudo apt-get install build-essential libssl-dev git -y
    git clone https://github.com/wg/wrk.git wrk
    cd wrk
    make
    # 把生成的wrk移到一个PATH目录下面, 比如
    sudo cp wrk /usr/local/bin
    ```

* Unbuntu/Debian下的安装
    ```bash
    sudo yum groupinstall 'Development Tools'
    sudo yum install openssl-devel
    sudo yum install git
    git clone https://github.com/wg/wrk.git wrk
    cd wrk
    make
    # 把生成的wrk移到一个PATH目录下面, 比如
    sudo cp wrk /usr/local/bin
    ```


### 命令行参数


```bash
使用方法: wrk <选项> <被测HTTP服务的URL>                            
Options:                                            
-c, --connections <N>  跟服务器建立并保持的TCP连接数量  
-d, --duration    <T>  压测时间           
-t, --threads     <N>  使用多少个线程进行压测
-s, --script      <S>  指定Lua脚本路径       
-H, --header      <H>  为每一个HTTP请求添加HTTP头      
    --latency          在压测结束后，打印延迟统计信息   
    --timeout     <T>  超时时间     
-v, --version          打印正在使用的wrk的详细版本信息
                                                      
<N>代表数字参数，支持国际单位 (1k, 1M, 1G)
<T>代表时间参数，支持时间单位 (2s, 2m, 2h)

# 例: 10并发 100连接数 持续访问30s
wrk -t10 -c100 -d30s http://127.0.0.1:8888
```

![](/image/性能工具wrk_001.png)

* Latency：响应时间
* Req/Sec：每个线程每秒钟的完成的请求数
* Avg：平均
* Max：最大
* Stdev：标准差
* +/- Stdev： 正负一个标准差占比


### Lua脚本个性化

wrk支持在三个阶段对压测进行个性化，分别是启动阶段、运行阶段和结束阶段。每个测试线程，都拥有独立的Lua运行环境。

![](/image/性能工具wrk_002.png)

* 1.启动阶段

    ```lua
    # 在脚本文件中实现setup方法，wrk就会在测试线程已经初始化但还没有启动的时候调用该方法。wrk会为每一个测试线程调用一次setup方法，并传入代表测试线程的对象thread作为参数。setup方法中可操作该thread对象，获取信息、存储信息、甚至关闭该线程。
    function setup(thread)
    -- thread提供了1个属性，3个方法
    -- thread.addr 设置请求需要打到的ip
    -- thread:get(name) 获取线程全局变量
    -- thread:set(name, value) 设置线程全局变量
    -- thread:stop() 终止线程
    ```

* 2.运行阶段

    ```lua
    function init(args)
    -- 每个线程仅调用1次，args 用于获取命令行中传入的参数, 例如 --env=pre

    function delay()
    -- 每次请求调用1次，发送下一个请求之前的延迟, 单位为ms

    function request()
    -- 每次请求调用1次，返回http请求

    function response(status, headers, body)
    -- 每次请求调用1次，返回http响应，如果没有定义该方法，那么wrk不会解析headers和body
    ```

* 3.结束阶段

    ```lua
    # 该方法在整个测试过程中只会调用一次，可从参数给定的对象中，获取压测结果，生成定制化的测试报告。
    function done(summary, latency, requests)

    latency.min              -- minimum value seen
    latency.max              -- maximum value seen
    latency.mean             -- average value seen
    latency.stdev            -- standard deviation
    latency:percentile(99.0) -- 99th percentile value
    latency(i)               -- raw value and count

    summary = {
      duration = N,  -- run duration in microseconds
      requests = N,  -- total completed requests
      bytes    = N,  -- total bytes received
      errors   = {
        connect = N, -- total socket connection errors
        read    = N, -- total socket read errors
        write   = N, -- total socket write errors
        status  = N, -- total HTTP status codes > 399
        timeout = N  -- total request timeouts
      }
    }
    ```

* 4.样例
    ```lua
    local counter = 1  
    local threads = {}  

    function setup(thread)  
       thread:set("id", counter)  
       table.insert(threads, thread)  
       counter = counter + 1  
    end  

    function init(args)  
       requests  = 0  
       responses = 0  
       local msg = "thread %d created"  
       print(msg:format(id))  
    end  

    function request()  
       requests = requests + 1  
    return wrk.request()  
    end  
    function response(status, headers, body)  
       responses = responses + 1  
    end  

    function done(summary, latency, requests)  
    for index, thread in ipairs(threads) do  
          local id        = thread:get("id")  
          local requests  = thread:get("requests")  
          local responses = thread:get("responses")  
          local msg = "thread %d made %d requests and got %d responses"  
          print(msg:format(id, requests, responses))  
       end  
    end
    ```

* 5.自定义脚本中可访问的变量和方法
    - wrk: 全局变量，修改后会影响所有请求
        ```lua
         wrk = {
            scheme  = "http",
            host    = "localhost",
            port    = nil,
            method  = "GET",
            path    = "/",
            headers = {},
            body    = nil,
            thread  = <userdata>,
          }
        ```
    - wrk.fomat:根据参数和全局变量wrk，生成整个request的string
        ```lua
        function wrk.format(method, path, headers, body)
        -- method: http方法, 如GET/POST/DELETE 等
        -- path:   url的路径, 如 /index, /index?a=b&c=d
        -- headers: 一个header的table
        -- body:    一个http body, 字符串类型
        ```
    - wrk.lookup:获取域名的IP和端口，返回table，例如：返回 `{127.0.0.1:80}`
        ```lua
        function wrk.lookup(host, service)
        -- host:一个主机名或者地址串(IPv4的点分十进制串或者IPv6的16进制串)
        -- service：服务名可以是十进制的端口号，也可以是已定义的服务名称，如ftp、http等
        ```
    - wrk.connect:判断addr是否能连接，例如：`127.0.0.1:80`，返回 true 或 false
        ```lua
        function wrk.connect(addr)
        ```


### Lua样例

* 压测支持HTTP pipeline的服务
    ```lua
    init = function(args)
       local r = {}
       r[1] = wrk.format(nil, "/?foo")
       r[2] = wrk.format(nil, "/?bar")
       r[3] = wrk.format(nil, "/?baz")

       req = table.concat(r)
    end

    request = function()
       return req
    end
    ```

* 认证之后获取token以进行压测
    ```lua
    token = nil
    path  = "/authenticate"

    request = function()
       return wrk.format("GET", path)
    end

    response = function(status, headers, body)
       if not token and status == 200 then
          token = headers["X-Token"]
          path  = "/resource"
          wrk.headers["X-Token"] = token
       end
    end
    ```

* 获取cookie以进行压测
    ```lua
    function getCookie(cookies, name)  
      local start = string.find(cookies, name .. "=")  
    if start == nil then  
    return nil  
      end  
    return string.sub(cookies, start + #name + 1, string.find(cookies, ";", start) - 1)  
    end  
    response = function(status, headers, body)  
      local token = getCookie(headers["Set-Cookie"], "token")  
    if token ~= nil then  
        wrk.headers["Cookie"] = "token=" .. token  
      end  
    end 
    ```

* 发送json
    ```lua
    request = function()
        local headers = { }
        headers['Content-Type'] = "application/json"
        body = {
            mobile={"1533899828"},
            params={code=math.random(1000,9999)}
        }

        local cjson = require("cjson")
        body_str = cjson.encode(body)
        return wrk.format('POST', nil, headers, body_str)
    end
    ```


More info: [wrk GitHub](https://github.com/wg/wrk)
