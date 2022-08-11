---
title: Golang（一）Golang的基本概念
date: 2021-02-15 22:23:32
tags: [golang]
copyright: true
password:
toc: true
---

　　Go语言（或 Golang）起源于 2007 年，并在 2009 年正式对外发布。Go 是 Google的 Robert Griesemer，Rob Pike 及 Ken Thompson 开发的一种静态强类型、编译型语言。它的主要目标是“兼具[Python](http://c.biancheng.net/python/)等动态语言的开发速度和 C/[C++](http://c.biancheng.net/cplus/)等编译型语言的性能与安全性”。
　　本文章主要介绍 Golang 的特点和部署使用。

<!--more-->

## Quick Guide

### 一、特点

- 类C语言：相似的表达式语法、控制流结构、基础数据类型、调用参数传值、指针等思想，还有编译后机器码的运行效率以及和现有操作系统的无缝适配。
- 不损失应用程序性能的情况下降低代码的复杂性，具有“部署简单、并发性好、语言设计良好、执行性能好”等优势
- 强大的网络编程和并发编程支持
- 没有类和继承的概念，通过接口（interface）的概念来实现多态性
  
### 二、优势

- [编程热度](https://www.tiobe.com/tiobe-index/)
- 开发和运行效率兼得:Go拥有接近C的运行效率和接近PHP的开发效率

![](/image/Golang01/Golang01_001.png)

- 简洁强大的并发:

![](/image/Golang01/Golang01_002.png)

- 学习难度低：类C的语法,如果熟悉C语言及其派生语言,一周就可以写出高性能的应用

### 三、安装部署

#### windows

例如window用户：

- 1.点击[官网](https://golang.google.cn/dl/)，选择对应系统包安装，点击下载

![](/image/Golang01/Golang01_003.png)

- 2.下载完一路点击安装就可以了。安装完成后，在安装目录下将生成一些目录和文件
- 3.设置环境变量
  - win+E,然后右键**这台电脑**→**属性**→**高级系统设置**→**环境变量**，如下图所示。
  - 在弹出的菜单里点击新建三个变量并配置到**Path**上。
    - **GOROOT**:刚才go的安装路径
    - **GOBIN**:go的执行程序路径
    - **GOPATH**:准备使用go进行开发的工程路径,
        
![](/image/Golang01/Golang01_004.png)
![](/image/Golang01/Golang01_005.png)



### 四、开发工具

1. Goland:是由 JetBrains 公司专门为开发者提供的一个符合人体工程学的商业 IDE。
2. LiteIDE:一款专门针对 Go 开发的集成开发环境，在编辑、编译和运行 Go 程序和项目方面都有非常好的支持。
3. Sublime Text:是一个革命性的跨平台（Linux、Mac OS X、Windows）文本编辑器，它支持编写非常多的编程语言代码。对于 Go 而言，它有一个插件叫做 GoSublime 来支持代码补全和代码模版。
4. GoClipse: Eclipse 的插件，拥有非常多的特性以及通过 GoCode 来实现代码补全功能。
5. VS Code: 是一款由微软公司开发的，能运行在 Mac OS X、Windows 和 Linux 上的跨平台开源代码编辑器

#### 使用

- 1.在自己建好的**GOPATH**下，新建三个目录
    - src 目录：放置项目和库的源文件；
    - pkg 目录：放置编译后生成的包/库的归档文件；
    - bin 目录：放置编译后生成的可执行文件
- 2.在src下面创建main目录,然后再目录下新建main.go,然后进行语言入门打卡操作
  
    ```go
    package main    // 声明 main 包
    import (
        "fmt"       // 导入 fmt 包，打印字符串是需要用到
    )
    func main() {   // 声明 main 主函数
        fmt.Println("Hello World!") // 打印 Hello World!
    }
    ```
    
- 3.编译和运行代码:如果是Goland使用ctrl+shift+F10,也可以使用下面命令:
    - go build fileName :将代码编译成二进制的可执行文件，但是需要手动运行该二进制文件
    - go run fileName :在编译后直接运行程序，编译过程中会产生一个临时文件，但不会生成可执行文件


### 五、命令工具

- go build：编译命令
  - -v: 编译时显示包名
  - -p n 开启并发编译，默认情况下该值为 CPU 逻辑核数
  - -a 强制重新构建
  - -n 打印编译时会用到的所有命令，但不真正执行
  - -x 打印编译时会用到的所有命令
  - -race 开启竞态检测
- go clean：清除编译文件
  - i 清除关联的安装的包和可运行文件，也就是通过go install安装的文件；
  - n 把需要执行的清除命令打印出来，但是不执行，这样就可以很容易的知道底层是如何运行的；
  - r 循环的清除在 import 中引入的包；
  - x 打印出来执行的详细命令，其实就是 -n 打印的执行版本；
  - cache 删除所有go build命令的缓存
  - testcache 删除当前包所有的测试结果
- go run：编译并运行
- go install：编译并安装
- go get：一键获取代码、编译并安装
  - -v 显示操作流程的日志及信息，方便检查错误
  - -u 下载丢失的包，但不会更新已经存在的包
  - -d 只下载，不安装
  - -insecure 允许使用不安全的 HTTP 方式进行下载操作
- go generate：在编译前自动化生成某类代码
  - run 正则表达式匹配命令行，仅执行匹配的命令；
  - v 输出被处理的包名和源文件名；
  - n 显示不执行命令；
  - x 显示并执行命令；
- go test：单元测试命令
- go fmt：格式化代码文件
  - -l 仅把那些不符合格式化规范的、需要被命令程序改写的源码文件的绝对路径打印到标准输出。而不是把改写后的全部内容都打印到标准输出。
  - -w 把改写后的内容直接写入到文件中，而不是作为结果打印到标准输出。
  - -r 添加形如“a[b:len(a)] -> a[b:]”的重写规则。如果我们需要自定义某些额外的格式化规则，就需要用到它。
  - -s 简化文件中的代码。
  - -d 只把改写前后内容的对比信息作为结果打印到标准输出。而不是把改写后的全部内容都打印到标准输出。 命令程序将使用 diff 命令对内容进行比对。在 Windows 操作系统下可能没有 diff 命令，需要另行 安装。
  - -e 打印所有的语法错误到标准输出。如果不使用此标记，则只会打印每行的第 1 个错误且只打印前 10 个错误。
  - -comments 是否保留源码文件中的注释。在默认情况下，此标记会被隐式的使用，并且值为 true。
  - -tabwidth 此标记用于设置代码中缩进所使用的空格数量，默认值为 8。要使此标记生效，需要使用“-tabs”标记并把值设置为 false。
  - -tabs 是否使用 tab（'\t'）来代替空格表示缩进。在默认情况下，此标记会被隐式的使用，并且值为 true。
  - -cpuprofile 是否开启 CPU 使用情况记录，并将记录内容保存在此标记值所指的文件中。
- go pprof：性能分析工具****

### 六、外部工具

#### **godoc**

godoc 工具会从 Go 程序和包文件中提取顶级声明的首行注释以及每个对象的相关注释，并生成相关文档，也可以作为一个提供在线文档浏览的 web 服务器，Go语言官网（[https://golang.google.cn/](https://golang.google.cn/)
）就是通过这种形式实现的。

```bash
go get golang.org/x/tools/cmd/godoc
```

##### 安装

由于防火墙的原因，国内的用户可能无法通过go get 命令来获取 godoc 工具，这时候就需要大家来手动操作了。

- 首先从 GitHub（[https://github.com/golang/tools.git](https://github.com/golang/tools.git)） 下载 golang.org/x/tools 包；
- 然后将下载得到的文件解压到 GOPATH 下的 src\golang.org\x\tools 目录中，没有的话可以手动创建；
- 打开 GOPATH 下的 src\golang.org\x\tools\cmd\godoc 目录，在该目录下打开命令行工具，并执行`go build` 命令，生成 godoc.exe 可执行文件；
- 最后，将生成的 godoc.exe 文件移动到 GOPATH 下的 bin 目录中。（需要把 GOPATH 下的 bin 目录添加到环境变量 Path 中）

##### 使用

完成上述操作后就可以使用 godoc 工具了，godoc 工具一般有以下几种用法：

- go doc package：获取包的文档注释，例如`go doc fmt` 会显示使用 godoc 生成的 fmt 包的文档注释；
- go doc package/subpackage：获取子包的文档注释，例如`go doc container/list`；
- go doc package function：获取某个函数在某个包中的文档注释，例如`go doc fmt Printf` 会显示有关 fmt.Printf() 的使用说明。

#### gofmt：go fmt的升级版

#### golint：代码质量的检查


More info: [Golang](http://c.biancheng.net/golang/)

