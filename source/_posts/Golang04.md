---
title: Golang（四）Golang的包管理
date: 2021-05-15 22:23:32
tags: [golang]
copyright: true
password:
toc: true
---

　　包是管理整个工程的工具。把同类型的文件放在一个目录，称之为 "包"，多个包构成 一个工程。 
　　本文章主要介绍 Golang 的包管理。

<!--more-->

## Quick Guide

### 一、包的规则

- 包名一般是小写的，使用一个简短且有意义的名称。
- 包名一般要和所在的目录同名，也可以不同，包名中不能包含``等特殊符号。
- 包一般使用域名作为目录名称，这样能保证包名的唯一性，比如 GitHub 项目的包一般会放到`GOPATH/src/github.com/userName/projectName`目录下。
- 包名为 main 的包为应用程序的入口包，编译不包含 main 包的源码文件时不会得到可执行文件。
- 一个文件夹下的所有源码文件只能属于同一个包。

### 二、自定义包

- 1.在 GOPATH 的 src 目录下创建一个文件（后缀必须是 .go）
- 2.文件开头都声明”package <包名,一般是目录名>“
- 3,定义包里面的函数,就完成了一个简单的包

![](/image/Golang04/Golang04_001.png)

### 三、包的导入

要在代码中引用其他包的内容，需要使用 import 关键字导入使用的包。具体语法如下：

```go
import "包的路径"
```

- import 导入语句通常放在源码文件开头包声明语句的下面；
- 导入的包名需要使用双引号包裹起来；
- 包名是从`GOPATH/src/` 后开始计算的，使用`/` 进行路径分隔。

```go
// 当行导入
import "包 1 的路径"
import "包 2 的路径"

// 多行导入
import (
    "包 1 的路径"
    "包 2 的路径"
)

// 绝对路径导入:以GOROOT/src/或GOPATH/src/的路径为起始点,计算被引用包的路径
import "database/sql"

// 相对路径导入:以引用的文件为起始点,计算被引用包的路径
import "../sql"
```

```jsx
package main    // 声明 main 包
import (
    "fmt"       // 导入 fmt 包，打印字符串是需要用到
    myfmt "mylib/fmt"  // 命名为 myfmt
)
func main() {   // 声明 main 主函数
    fmt.Println("Hello World!") // 打印 Hello World!
    myfmt.Println("Hello World again!")
}
```

### 四、包的引用格式

包的引用有四种格式，下面以 fmt 包为例来分别演示一下这四种格式。

- 标准引用格式

```go
package main

import "fmt"

func main() {
    fmt.Println("标准引用")
}
```

- 自定义别名引用格式

```go
package main

import F "fmt"

func main() {
    F.Println("自定义别名引用")
}
```

- 省略引用格式

```go
package main

import . "fmt"

func main() {
    //不需要加前缀 fmt.
    Println("省略引用")
}
```

- 匿名引用格式：只执行包初始化的 init 函数，而不使用包内部的数据

```go
package main

import (
    _ "database/sql"
    "fmt"
)

func main() {
    fmt.Println("匿名引用")
}
```

### 五、包的加载

当使用main启动这个程序的时候，包就会加载起来，过程如下图：

![](/image/Golang04/Golang04_002.png)

### 六、常用的包

接下来给大家列一下常用的内置包，可以方便大家使用，省的还需要自己去定义。

- 1.fmt：格式化的标准输入输出
    - Printf() ：输出后换行
    - Println() ：格式化输出
- 2.io：提供了原始的 I/O 操作界面
- 3.bufio：各个组件内部都维护了一个缓冲区，数据读写操作都直接通过缓存区进行 bufio 包通过对 io 包的封装，提供了数据缓冲功能，能够一定程度减少大块数据读写带来的开销。
- 4.sort：提供了用于对切片和用户定义的集合进行排序的功能。
- 5.strconv：提供了将字符串转换成基本数据类型，或者从基本数据类型转换为字符串的功能。
- 6.os：提供了不依赖平台的操作系统函数接口
    - Hostname():返回内核提供的主机名
    - Environ():返回所有的环境变量，返回值格式为“key=value”的字符串的切片拷贝。
    - Getenv():会检索并返回名为 key 的环境变量的值。如果不存在该环境变量则会返回空字符串。
    - Setenv():设置名为 key 的环境变量，如果出错会返回该错误。
    - Exit():当前程序以给出的状态码 code 退出。
    - Getwd():回一个对应当前工作目录的根路径。
    - Mkdir():可以使用指定的权限和名称创建一个目录。
    - MkdirAll():可以使用指定的权限和名称创建一个目录，包括任何必要的上级目录，并返回 nil，否则返回错误。
    - Remove():会删除 name 指定的文件或目录。
    - RemoveAll ():会递归的删除所有子目录和文件。
- 7.os/exec：提供了执行自定义 linux 命令的相关实现。
- 8.sync：多线程中锁机制以及其他同步互斥机制
    - Mutex:互斥锁
    - RWMutex：读写锁
- 9.flag：提供命令行参数的规则定义和传入参数解析的功能
- 10.encoding/json：JSON的序列号和反序列化
- 11.html/template：web 开发中生成 html 的 template 的一些函数
- 12.net/http：提供 HTTP 相关服务，主要包括 http 请求、响应和 URL 的解析，以及基本的 http 客户端和扩展的 http 服务。
- 13.reflect：提供运行时反射，允许程序通过抽象类型操作对象。
- 14.strings和bytes：提供处理字符串的一些函数集合，包括合并、查找、分割、比较、后缀检查、索引、大小写处理等等。
- 15.log：用于在程序中输出日志
    - Print(): 普通输出；
    - Fatal(): 在执行完 Print 后，执行 os.Exit(1)；
    - Panic():在执行完 Print 后调用 panic() 方法。
- 16.math/big：实现了大数字的多精度计算
    - Int:有符号整数
    - Rat:有理数
    - Float:浮点数
- 17.regexp:正则表达式

```go
package main
import (
	"fmt"
	"regexp"
)
func main() {
	buf := "abc azc a7c aac 888 a9c  tac"
	//解析正则表达式，如果成功返回解释器
	reg1 := regexp.MustCompile(`a.c`)
	if reg1 == nil {
		fmt.Println("regexp err")
		return
	}
	//根据规则提取关键信息
	result1 := reg1.FindAllStringSubmatch(buf, -1)
	fmt.Println("result1 = ", result1)
}
```

- 18.time：时间显示和测量等所用的函数
    - Now()：当前时间
    - Add() :增加时间
    - Sub():时间相减
    - ParseInLocation():字符串转为本地时间
    - Pta
- 19.flag：给命令行参数增加描述

### 七、第三方包的管理

**go module** 是Go语言默认的依赖管理工具。除此之外,还有godep、glide和govendor，这边就不过多描述。

常用命令如下:

- 1.准备工作，先设置代理

```go
// Windows 下设置 GOPROXY 的命令为
go env -w GOPROXY=https://goproxy.cn,direct
// MacOS 或 Linux 下设置 GOPROXY 的命令为：
export GOPROXY=https://goproxy.cn
```

- 2.在 GOPATH 目录之外新建一个工程目录，并使用go mod init初始化生成 go.mod 文件。

```go
go mod init hello
```

go.mod文件内容：

```go
module go_mod

go 1.15
```

- 3.创建一个go文件，然后增加依赖引用，并运行它。它就会去自动下载需要的第三方包，放到 GOPATH目录下pkg/mod,并且会更新 go.mod文件。

```go
package main
import (
	"github.com/labstack/echo"
	"net/http"
)
func main() {
	e := echo.New()
	e.GET("/", func(c echo.Context) error {
		return c.String(http.StatusOK, "Hello World!")
	})
}
```

go.mod文件内容：

```go
module go_mod

go 1.15

require (
	github.com/labstack/echo v3.3.10+incompatible
	github.com/labstack/gommon v0.3.0 // indirect
	golang.org/x/crypto v0.0.0-20200820211705-5c72a883971a // indirect
)
```

go.mod 提供了 module、require、replace 和 exclude 四个命令：

- module 语句指定包的名字（路径）；
- require 语句指定的依赖项模块；
- replace 语句可以替换依赖项模块；
- exclude 语句可以忽略依赖项模块。


More info: [Golang](http://c.biancheng.net/golang/)
