---
title: Golang（三）Go语言的基本语法(下)
date: 2021-04-15 22:23:32
tags: [golang]
copyright: true
password:
toc: true
---

　　本文章主要介绍 Golang 的基本语法。

<!--more-->

## Quick Guide

### 一、容器
    
复杂类型的变量,具有各种形式的存储和处理数据的功能,主要用于编写复杂算法、结构和逻辑。
    
#### 数组
    
数组是一个由固定长度的特定类型元素组成的序列，一个数组可以由零个或多个元素组成。

声明语法如下：

```go
var 数组变量名 [元素数量]Type
```

- 数组变量名：数组声明及使用时的变量名。
- 元素数量：数组的元素数量，可以是一个表达式，但最终通过编译期计算的结果必须是整型数值，元素数量不能含有到运行时才能确认大小的数值。
- Type：可以是任意基本类型，包括数组本身，类型为数组本身时，可以实现多维数组。

```go
package main

import (
  "fmt"
)

func main() {

  var a [3]int             // 定义三个整数的数组
    // 访问数组的每个元素可以通过索引下标，索引下标的范围是从 0 开始到数组长度减 1 的位置，内置函数 len() 可以返回数组中元素的个数。
  fmt.Println(a[0])        // 打印第一个元素
  fmt.Println(a[len(a)-1]) // 打印最后一个元素

  // 遍历数组——访问每一个数组元素，打印索引和元素
  for i, v := range a {
    fmt.Printf("%d %d\n", i, v)
  }

    // 如果在数组长度的位置出现“...”省略号，则表示数组的长度是根据初始化值的个数来计算
    q := [...]int{1, 2, 3}
    fmt.Printf("%T\n", q) // "[3]int"
}
```

**默认情况下，数组的每个元素都会被初始化为元素类型对应的零值。**

##### 数组之间的对比

可以直接通过较运算符 ==和!=

```go
package main

import (
  "fmt"
)

func main() {
    a := [2]int{1, 2}
    b := [...]int{1, 2}
    c := [2]int{1, 3}
    fmt.Println(a == b, a == c, b == c) // "true false false"
    d := [3]int{1, 2}
    fmt.Println(a == d) // 编译错误：无法比较 [2]int == [3]int
}
```

##### 多维数组

声明语法如下：

```go
var array_name [size1][size2]...[sizen] array_type
```

- array_name 为数组的名字
- array_type 为数组的类型
- size1、size2 等等为数组每一维度的长度。

```go
package main

import (
  "fmt"
)

func main() {
    // 声明一个二维整型数组，两个维度的长度分别是 4 和 2
    var array [4][2]int
    // 使用数组字面量来声明并初始化一个二维整型数组
    array = [4][2]int{{10, 11}, {20, 21}, {30, 31}, {40, 41}}
    // 声明并初始化数组中索引为 1 和 3 的元素
    array = [4][2]int{1: {20, 21}, 3: {40, 41}}
}
```

#### 切片

切片（slice）是对数组的一个连续片段的**引用**,就像切糕一样,把数组切出几块,取出其中一块.

语法如下：

```go
slice [开始位置 : 结束位置]
```

- slice：表示目标切片对象；
- 开始位置：对应目标切片对象的索引；
- 结束位置：对应目标切片的结束索引。

```go
package main

import (
  "fmt"
)

func main() {
    var a  = [3]int{1, 2, 3}
    fmt.Println(a, a[1:2]) // 结果:[1 2 3]  [2]
}
```
    

切片规则

- 取出的元素数量为：结束位置 - 开始位置；
- 取出元素不包含结束位置对应的索引，切片最后一个元素使用 slice[len(slice)] 获取；
- 当缺省开始位置时，表示从连续区域开头到结束位置；
- 当缺省结束位置时，表示从开始位置到整个连续区域末尾；
- 两者同时缺省时，与切片本身等效；
- 两者同时为 0 时，等效于空切片，一般用于切片复位。

```go
package main

import (
	"fmt"
)

func main() {
    var highRiseBuilding [30]int
    for i := 0; i < 30; i++ {
            highRiseBuilding[i] = i + 1
    }
    // 区间
    fmt.Println(highRiseBuilding[10:15])
    // 中间到尾部的所有元素
    fmt.Println(highRiseBuilding[20:])
    // 开头到中间指定位置的所有元素
    fmt.Println(highRiseBuilding[:2])
}
```

##### 声明切片

声明语法如下：

```go
var name []Type
make( []Type, size, cap )
// make函数用于初始化slice、chan和map
// 如果只用var声明，不用make初始化，变量对应的值为nil。
// size 元素的个数
// cap 从它的第一个元素开始数，到其底层数组元素末尾的个数

// 例子
package main

import (
	"fmt"
)

func main() {
    // 声明字符串切片
    var strList []string
    // 声明整型切片
    var numList []int
    // 声明一个空切片
    var numListEmpty = []int{}
    // 输出3个切片
    fmt.Println(strList, numList, numListEmpty)
	
	a := make([]int, 2)
    b := make([]int, 2, 10)
    fmt.Println(a, b)
    fmt.Println(len(a), len(b)
}
```

##### 切片扩容

```go
package main

import (
	"fmt"
)

func main() {
    // 扩展元素,cap不足,低于1000一下是翻倍扩展,大于等于1.25倍增加
    var a []int
    a = append(a, 1) // 追加1个元素
    fmt.Println(a)
    a = append(a, 1, 2, 3) // 追加多个元素, 手写解包方式
    fmt.Println(a)
    a = append(a, []int{1,2,3}...) // 追加一个切片, 切片需要解包
    fmt.Println(a)
}
```

##### 切片删除元素

```go
package main

import (
	"fmt"
)

func main() {
    a = []int{1, 2, 3}
	a = a[1:] // 删除开头1个元素
	a = append(a[:2], a[2+1:]...) // 删除中间1个元素
	a = a[:3-1] // 删除尾部1个元素
}
```

##### 切片复制

语法如下：

```go
copy( destSlice, srcSlice []T) int

// 例子
package main

import (
	"fmt"
)

func main() {
    slice1 := []int{1, 2, 3, 4, 5}
    slice2 := []int{5, 4, 3}
    copy(slice2, slice1) // 只会复制slice1的前3个元素到slice2中
    copy(slice1, slice2) // 只会复制slice2的3个元素到slice1的前3个位置
}
```

##### 多维切片

语法如下：

```go
var sliceName [][]...[]sliceType
```

![](/image/Golang03/Golang03_001.png)

#### 映射

map是一种元素对（pair）的无序集合，pair 对应一个 key（索引）和一个 value（值），所以这个结构也称为关联数组或字典。

声明语法如下：

```go
var mapname map[keytype]valuetype
make(map[keytype]valuetype, cap)

```

- mapname 为 map 的变量名。
- keytype 为键类型。
- valuetype 是键对应的值类型。
- cap 预设的容量。

```go
package main

import "fmt"

func main() {
	mapLit := map[string]int{"one": 1, "two": 2}
	mapCreated := make(map[string]float32)
	mapCreated["key1"] = 4.5
	mapCreated["key2"] = 3.14159
	mapLit["two"] = 3
	fmt.Printf("Map literal at \"one\" is: %d\n", mapLit["one"])
	fmt.Printf("Map created at \"key2\" is: %f\n", mapCreated["key2"])
	fmt.Printf("Map assigned at \"two\" is: %d\n", mapLit["two"])
	fmt.Printf("Map literal at \"ten\" is: %d\n", mapLit["ten"])
}
```

##### map的高级用法

```go
package main

import "fmt"

func main() {
	// 声明
	scene := make(map[string]int)
	// 初始化
  scene["route"] = 66
  scene["brazil"] = 4
	scene["china"] = 960
	// 遍历
  for k, v := range scene {
        fmt.Println(k, v)
	}

	// 删除指定key
	delete(scene, "brazil")
	fmt.Println(scene)
}
```

#### 列表

list是一种非连续的存储容器，由多个节点组成，节点通过变量记录彼此之间的关系，列表有多种实现方法，如单链表、双链表等。

列表的原理可以这样理解：假设 A、B、C 三个人都有电话号码，如果 A 把号码告诉给 B，B 把号码告诉给 C，这个过程就建立了一个单链表结构，如下图所示。

![](/image/Golang03/Golang03_002.png)

如果在这个基础上，再从 C 开始将自己的号码告诉给自己所知道号码的主人，这样就形成了双链表结构，如下图所示。

![](/image/Golang03/Golang03_003.png)

那么如果需要获得所有人的号码，只需要从 A 或者 C 开始，要求他们将自己的号码发出来，然后再通知下一个人如此循环，这样就构成了一个列表遍历的过程。

如果 B 换号码了，他需要通知 A 和 C，将自己的号码移除，这个过程就是列表元素的删除操作，如下图所示。

![](/image/Golang03/Golang03_004.png)

##### 列表的初始化

- 1.通过 container/list 包的 New() 函数初始化 list

```go
变量名 := list.New()
```

- 2.通过 var 关键字声明初始化 list

```go
var 变量名 list.List
```

##### 遍历列表

遍历双链表需要配合 Front() 函数获取头元素，遍历时只要元素不为空就可以继续进行，每一次遍历都会调用元素的 Next() 函数

```go
package main

import (
	"container/list"
	"fmt"
)

func main() {
	// 创建一个 list
	l := list.New()
	//把4元素放在最后
	e4 := l.PushBack(4)
	//把1元素放在最前
	e1 := l.PushFront(1)
	// 遍历所有元素并打印其内容
	for e := l.Front(); e != nil; e = e.Next() {
		fmt.Println(e.Value)
	}
}
```

##### 在列表中插入元素

| 方 法 | 功 能 |
| --- | --- |
| InsertAfter(v interface {}, mark * Element) * Element | 在 mark 点之后插入元素，mark 点由其他插入函数提供 |
| InsertBefore(v interface {}, mark * Element) *Element | 在 mark 点之前插入元素，mark 点由其他插入函数提供 |
| PushBackList(other *List) | 添加 other 列表元素到尾部 |
| PushFrontList(other *List) | 添加 other 列表元素到头部 |

```go
package main

import (
	"container/list"
	"fmt"
)

func main() {
	// 创建一个 list
	l := list.New()
	//把4元素放在最后
	e4 := l.PushBack(4)
	//把1元素放在最前
	e1 := l.PushFront(1)
	//在e4元素前面插入3
	l.InsertBefore(3, e4)
	//在e1后面插入2
	l.InsertAfter(2, e1)
	// 遍历所有元素并打印其内容
	for e := l.Front(); e != nil; e = e.Next() {
		fmt.Println(e.Value)
	}
}
```

##### 从列表中删除元素

列表插入函数的返回值会提供一个 *list.Element 结构，这个结构记录着列表元素的值以及与其他节点之间的关系等信息，从列表中删除元素时，需要用到这个结构进行快速删除。

直接看例子:

```go
package main

import (
	"container/list"
	"fmt"
)

func main() {
	l := list.New()
	// 尾部添加
	l.PushBack("canon")
	// 头部添加
	l.PushFront(67)
	// 尾部添加后保存元素句柄
	element := l.PushBack("fist")
	// 在fist之后添加high
	l.InsertAfter("high", element)
	// 在fist之前添加noon
	l.InsertBefore("noon", element)
	// 遍历所有元素并打印其内容
	for e := l.Front(); e != nil; e = e.Next() {
		fmt.Println(e.Value)
	}
	// 使用
	l.Remove(element)
	fmt.Println("删除后")
	// 遍历所有元素并打印其内容
	for e := l.Front(); e != nil; e = e.Next() {
		fmt.Println(e.Value)
	}
}
```

### 二、结构体

结构体是一种复合类型，由零个或多个任意类型的值聚合成的实体，每个值都可以称为结构体的成员。

定义如下：

```go
type 类型名 struct {
    字段1 字段1类型
    字段2 字段2类型
    …
}

```

- 类型名：标识自定义结构体的名称，在同一个包内不能重复。
- struct{}：表示结构体类型
- 字段1、字段2……：表示结构体字段名，结构体中的字段名必须唯一。
- 字段1类型、字段2类型……：表示结构体各个字段的类型,可以是结构体。

#### 实例化

```go
package main

import "fmt"

func main() {
  // 定义只是一种内存布局的描述，只有当实例化时，才会真正地分配内存
	type Point struct {
		X int
		Y int
	}
  // 实例化
	var p Point
	// 用.访问
	p.X = 10
	p.Y = 20

	fmt.Println(p.X)
	fmt.Println(p.Y)
}
```

还可以通过以下两种方式实例化：

```go
ins := new(T)
ins := &T{}

```

- T 表示结构体类型
- ins：T 类型被实例化后保存到 ins 变量中，ins 的类型为 *T，属于指针。

#### 初始化

```go
ins := 结构体类型名{
    字段1: 字段1的值,
    字段2: 字段2的值,
    …
}

ins := 结构体类型名{
    字段1的值,
    字段2的值,
    …
}
```

```go
import "fmt"

func main(){
	type People struct {
		name  string
	}
	relation := &People{
		name: "爷爷",
	}

type Address struct {
		Province    string
	}
	addr := Address{
		"四川",
	}
	fmt.Println(relation.name)
	fmt.Println(addr.Province)
}
```

#### 匿名结构体

```go
ins := struct {
    // 匿名结构体字段定义
    字段1 字段类型1
    字段2 字段类型2
    …
}{
    // 字段值初始化
    初始化字段1: 字段1的值,
    初始化字段2: 字段2的值,
    …
}
```

```go
package main

import (
"fmt"
)

func main() {
	// 实例化一个匿名结构体
	msg := &struct {  // 定义部分
		id   int
		data string
	}{  // 值初始化部分
		1024,
		"hello",
	}
	fmt.Println(msg.id)
	fmt.Println(msg.data)
}
```

### 三、接口

接口是一组方法的集合，可以理解为抽象的类型。它提供了一种非侵入式的接口。任何类型只要实现了该接口中方法集，那么就属于这个类型。

接口声明的格式:

```go
type 接口类型名 interface{
    方法名1( 参数列表1 ) 返回值列表1
    方法名2( 参数列表2 ) 返回值列表2
    …
}
```

- 接口类型名：使用 type 将接口定义为自定义的类型名。Go语言的接口在命名时，一般会在单词后面添加 er，如有写操作的接口叫 Writer
- 方法名：当方法名首字母是大写时，且这个接口类型名首字母也是大写时，这个方法可以被接口所在的包（package）之外的代码访问。（小写屏蔽隐藏机制）
- 参数列表、返回值列表：参数列表和返回值列表中的参数变量名可以被忽略

```go
package main

import "fmt"

// 定义一个鸭子接口
type Duck interface {
	Quack()   // 鸭子叫
	DuckGo()  // 鸭子走
}

// 现在有只鸡类型
type Chicken struct {
}

func (c Chicken) IsChicken() {
	fmt.Println("我是小鸡")
}

// 这只鸡会鸭子叫和鸭子走
func (c Chicken) Quack() {
	fmt.Println("嘎嘎")
}

func (c Chicken) DuckGo() {
	fmt.Println("大摇大摆的走")
}

// 定义一个函数，负责执行鸭子能做的事情
func DoDuck(d Duck) {
	d.Quack()
	d.DuckGo()
}

func main() {
	c := Chicken{}
	DoDuck(c)
}
```

- 接口的方法 与 实现接口的类型方法格式一致
- 接口中所有方法均被实现

#### 类型断言

如果想判断 一个使用在接口值上的操作，用于检查接口类型变量所持有的值是否实现了期望的接口或者具体的类型。

```go
value, ok := x.(T)
```

- x 表示一个接口的类型
- T 表示一个具体的类型（也可为接口类型）

```go
package main

import (
	"fmt"
)

func main() {
  // 可以接受任何类型的数据
	var x interface{}
	x = 10
	value1, ok1 := x.(int)
	fmt.Print(value1, ",", ok1, "\n")

	x = nil
	value2, ok2 := x.(int)
	fmt.Print(value2, ",", ok2, "\n")

}

func getType(a interface{}) {
    switch a.(type) {
    case int:
        fmt.Println("the type of a is int")
    case string:
        fmt.Println("the type of a is string")
    case float64:
        fmt.Println("the type of a is float")
    default:
        fmt.Println("unknown type")
    }
}

func main() {
    var a int
    a = 10
    getType(a)
}
```

#### 接口排序

其实可以用来排序。内置接口 sort.Interface,它需要知道三个东西：序列的长度，表示两个元素比较的结果，一种交换两个元素的方式,它就会给你排序

```go
package main

import (
	"fmt"
	"sort"
)

// 将[]string定义为MyStringList类型
type MyStringList []string

// 实现sort.Interface接口的获取元素数量方法
func (m MyStringList) Len() int {
	return len(m)
}

// 实现sort.Interface接口的比较元素方法
func (m MyStringList) Less(i, j int) bool {
	return m[i] < m[j]
}

// 实现sort.Interface接口的交换元素方法
func (m MyStringList) Swap(i, j int) {
	m[i], m[j] = m[j], m[i]
}
func main() {
	// 准备一个内容被打乱顺序的字符串切片
	names := MyStringList{
		"3. Triple Kill",
		"5. Penta Kill",
		"2. Double Kill",
		"4. Quadra Kill",
		"1. First Blood",
	}
	// 使用sort包进行排序
	sort.Sort(names)
	// 遍历打印结果
	for _, v := range names {
		fmt.Printf("%s\n", v)
	}
}
```

### 四、进程

**进程**：是程序在操作系统中的一次执行过程，系统进行资源分配和调度的一个独立单位。 

**线程**：是进程的一个执行实体，是 CPU 调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。 一个进程可以创建和撤销多个线程，同一个进程中的多个线程之间可以并发执行。

![](/image/Golang03/Golang03_005.png)

**协程**：协程是一种用户态的轻量级线程，由用户控制协程的调度。线程进程都是同步机制，而协程则是异步，只不过协程能保留上一次调用时的状态，每次切换回来时，就相当于进入上一次调用的状态。

![](/image/Golang03/Golang03_006.png)

**并发**： 多线程程序在单核心的 cpu 上运行，取得多个任务，利用时序切换不同任务执行.请看下图：

![](/image/Golang03/Golang03_007.png)

**并行**： 多线程程序在多核心的 cpu 上运行.取得多个任务，并同时去执行所取得的这些任务。相当于将长长的一条队列，划分成了多条短队列，所以并行缩短了任务队列的长度。请看下图：

![](/image/Golang03/Golang03_008.png)

#### goroutine

go 并发是 让某个函数独立运行的能力，这个核心就是goroutine。goroutine有点类似协程，一个goroutine就是一个独立的工作单元，运行时通过算法调度这些goroutine来运行，在单个进程里执行成千上万的并发任务。

语法如下：

```go
go 函数名( 参数列表 )
```

- 函数名：要调用的函数名。
- 参数列表：调用函数需要传入的参数。

```go
package main
import (
	"fmt"
	"time"
)
func running() {
	var times int
	// 构建一个无限循环
	for {
		times++
		fmt.Println("tick", times)
		// 延时1秒
		time.Sleep(time.Second)
	}
}
func main() {
	// 并发执行程序
	go running()

    // 接受命令行输入, 不做任何事情
    var input string
    fmt.Scanln(&input)
}
```

#### 使用匿名函数创建goroutine

语法如下：

```go
go func( 参数列表 ){
    函数体
}( 调用参数列表 )
```

- 参数列表：函数体内的参数变量列表。
- 函数体：匿名函数的代码。
- 调用参数列表：启动 goroutine 时，需要向匿名函数传递的调用参数。

```go
package main
import (
    "fmt"
    "time"
)
func main() {
    go func() {
        var times int
        for {
            times++
            fmt.Println("tick", times)
            time.Sleep(time.Second)
        }
    }()
    var input string
    fmt.Scanln(&input)
}
```

- 1.一个是主进程执行过快，导致其他协程没有执行；
- 2.多个协程之间用到相同的数据；

#### 等待组

| 方法名 | 功能 |
| --- | --- |
| (wg * WaitGroup) Add(delta int) | 等待组的计数器 +1 |
| (wg * WaitGroup) Done() | 等待组的计数器 -1 |
| (wg * WaitGroup) Wait() | 当等待组计数器不等于 0 时阻塞直到变 0。 |

使用步骤：

- 1.利用wg.Add(delta)先增加计数器的个数
- 2.再利用wg.Done()减少计数器的个数，最后让计数器等于0
- 3.当等待组计数器等于0，才会执行wg.Wait()后面的代码，不然就一直阻塞

```go
package main
import (
	"fmt"
	"net/http"
	"sync"
)
func main() {
	// 声明一个等待组
	var wg sync.WaitGroup
	// 准备一系列的网站地址
	var urls = []string{
		"https://www.baidu.com/",
		"https://www.sougou.com/",
	}
	// 遍历这些地址
	for _, url := range urls {
		// 每一个任务开始时, 将等待组增加1
		wg.Add(1)
		// 开启一个并发
		go func(url string) {
			// 使用defer, 表示函数完成时将等待组值减1
			defer wg.Done()
			// 使用http访问提供的地址
			_, err := http.Get(url)
			// 访问完成后, 打印地址和可能发生的错误
			fmt.Println(url, err)
			// 通过参数传递url地址
		}(url)
	}
	// 等待所有的任务完成
	wg.Wait()
	fmt.Println("over")
}
```

#### 资源竞争

```go
package main
import (
	"fmt"
	"runtime"
	"sync"
)
var (
	count int32
	wg    sync.WaitGroup
)
func main() {
	wg.Add(2)
	go incCount()
	go incCount()
	wg.Wait()
	fmt.Println(count)
}
func incCount() {
	defer wg.Done()
	for i := 0; i < 2; i++ {
		fmt.Println("count:",count)
		value := count
		// 是让当前 goroutine 暂停的意思，退回执行队列，让其他等待的 goroutine 运行，目的是为了使资源竞争的结果更明显。
		runtime.Gosched()
		value++
		count = value
	}
}
```

预期是4,实际结果 2/3/4之间随机出现. 因为 count 变量没有任何同步保护，所以两个 goroutine 都会对其进行读写，会导致对已经计算好的结果被覆盖，以至于产生错误结果。

##### 锁住共享资源

解决方案1:锁住共享资源

- 原子函数: 以很底层的加锁机制来同步访问整型变量和指针
    - atomic.AddInt64 : 安全地加一个整型值的方式
    - atomic.LoadInt64 : 安全地读一个整型值的方式
    - atomic.StoreInt64 : 安全地写一个整型值的方式

```go
package main
import (
	"fmt"
	"runtime"
	"sync"
	"sync/atomic"
)
var (
	counter int64
	wg      sync.WaitGroup
)
func main() {
	wg.Add(2)
	go incCounter(1)
	go incCounter(2)
	wg.Wait() //等待goroutine结束
	fmt.Println(counter)
}
func incCounter(id int) {
	defer wg.Done()
	for count := 0; count < 2; count++ {
		//安全的对counter加1
		atomic.AddInt64(&counter, 1) 
		fmt.Println("counter:",counter)
		runtime.Gosched()
	}
```

##### 互斥锁

方案2:使用互斥锁。

- 互斥锁:在代码上创建一个临界区，保证同一时间只有一个 goroutine 可以执行这个临界代码。
    - sync.Mutex：暴力锁， 当一个 goroutine 获得了 Mutex 后，其他 goroutine 就只能乖乖等到这个 goroutine 释放该 Mutex。
        - Lock() 加锁
        - Unlock() 解锁
    - sync.RWMutex： 基于sync.Mutex产生的单写多读模型，运行多个 goroutine 读，读的时候不允许写入，写的时候不允许读。
        - Lock()和Unlock()用于申请和释放写锁
        - RLock()和RUnlock()用于申请和释放读锁

```go
package main
import (
	"fmt"
	"runtime"
	"sync"
)
var (
	counter int64
	wg      sync.WaitGroup
	mutex   sync.Mutex
)
func main() {
	wg.Add(2)
	go incCounter(1)
	go incCounter(2)
	wg.Wait()
	fmt.Println(counter)
}
func incCounter(id int) {
	defer wg.Done()
	for count := 0; count < 2; count++ {
		//同一时刻只允许一个goroutine进入这个临界区
		mutex.Lock()
		{
			value := counter
			runtime.Gosched()
			value++
			counter = value
		}
		mutex.Unlock() //释放锁，允许其他正在等待的goroutine进入临界区
	}
}
```

#### channel

![](/image/Golang03/Golang03_009.png)

通道（channel）是一种特殊的类型。在任何时候，同时只能有一个 goroutine 访问通道进行发送和获取数据。goroutine 间通过通道就可以通信。

通道像一个传送带或者队列，总是遵循先入先出（First In First Out）的规则，保证收发数据的顺序。

声明语法如下：

```go
var 通道变量 chan 通道类型
```

- 通道类型：通道内的数据类型。
- 通道变量：保存通道的变量。

创建语法如下：

```go
通道实例 := make(chan类型 通道类型, 缓冲大小)
```

- chan类型：
    - chan<- 只能用来发送
    - <-chan 只能用来接收
    - chan 用来发送和接收
- 通道类型：和无缓冲通道用法一致，影响通道发送和接收的数据类型。
- 缓冲大小：决定通道最多可以保存的元素数量。
    - **无缓冲通道**：不设置。进行发送 goroutine 需要被接收后才可以继续发送。接收的goroutine 也同理。
    - **缓冲通道**：设置大小，缓存大小为设置个数。进行发送goroutine 可以在发送元素达到缓存上限之前，继续发。接收的goroutine 需要通道元素不为零，就可以一直接收。
- 通道实例：被创建出的通道实例。

```go
package main

import "fmt"

func main() {
	senderOnly := make(chan<- int)   // 只能用来发送（管道的入口，只进不出）
	receiverOnly := make(<-chan int) // 只能用来接收（管道的出口，只出不进）
	unbuffer := make(chan int)       // 无缓冲可收发
	buffer := make(chan int, 2)      // 无缓冲可收发
	fmt.Println(senderOnly, receiverOnly, unbuffer, buffer)
}
```

- 使用通道收发数据:

```go
通道变量 <- 值
收到的值 := <-通道变量
```

```go
package main

import "fmt"

func main() {
	fmt.Println("start main")
    // 创建通道
	ch := make(chan int)

	var result int
	go func() {
		println("come into goroutine1")
		var r int
		for i := 1; i <= 3; i++ {
			r += i
		}

        // 发送数据到通道
		ch <- r
	}()

	go func() {
		println("come into goroutine2")
		var r int = 1
		for i := 1; i <= 3; i++ {
			r *= i
		}
        // 发送数据到通道
		ch <- r
	}()

	go func() {
		println("come into goroutine3")
        // 发送数据到通道
		ch <- 11
	}()

	for i := 0; i < 3; i++ {
        // 接受数据并累加
		result += <-ch
	}
	close(ch)
	fmt.Println("result is:", result)
	fmt.Println("end main")
}
```

```go
package main

import (
	"fmt"
)

func main() {
	fmt.Println("start main")
	// 创建一个3个元素缓冲大小的整型通道
	ch := make(chan int, 3)
	// 查看当前通道的大小
	fmt.Println("通道的大小:",len(ch))
	// 开启一个并发匿名函数
	// 开启一个并发匿名函数
	ch <- 1
	ch <- 2
	ch <- 3
	fmt.Println("通道的大小:",len(ch))
	// 遍历接收通道数据
	for data := range ch {
		// 打印通道数据
		fmt.Println(data)
		// 当遇到数据0时, 退出接收循环
		if data == 3 {
			break
		}
	}
	fmt.Println("end main")
}
```

##### 超时通道

因为发送元素到通道,如果没有及时被接收,就会造成阻塞.所以我们可以结合select进行超时判断:

语法结构如下:

```go
select {
    case <-chan1:
    // 如果chan1成功读到数据，则进行该case处理语句
    case chan2 <- 1:
    // 如果成功向chan2写入数据，则进行该case处理语句
    default:
    // 如果上面都没有成功，则进入default处理流程
}
```

```go
package main
import (
	"fmt"
	"time"
)
func main() {
	// 创建普通通道
	ch := make(chan int)
	// 创建超时通道
	quit := make(chan bool)
	//新开一个协程
	go func() {
		for {
			select {
			case num := <-ch:
				fmt.Println("num = ", num)
			case <-time.After(3 * time.Second):
				// 经过了3秒
				fmt.Println("超时")
				quit <- true
			}
		}
	}()
	for i := 0; i < 5; i++ {
		ch <- i
		// 等待1秒再读取
		time.Sleep(time.Second)
	}
	// 从超时通道获取到信息，退出进程
	<-quit
	fmt.Println("程序结束")
}
```

#### 控制性能

使用下面命令设置程序运行占用的cpu核数。（默认使用机器的最大核数）

```go
// 程序运行占用的cpu核数
runtime.GOMAXPROCS(逻辑CPU数量)
// 查询机器的cpu核数
runtime.NumCPU()
```

逻辑CPU的数量：

- <1：不修改任何数值。
- =1：单核心执行。
- >1：多核并发执行。

### 五、reflect

程序在编译时变量被转换为内存地址，变量名不会被编译器写入到可执行部分，所以在运行程序时程序无法获取自身的信息。但是 **反射** 可以在程序运行期对程序本身进行访问和修改。

| 类型 | 作用 |
| --- | --- |
| reflect.ValueOf() | 获取输入参数接口中的数据的值，如果为空则返回0 <- 注意是0 |
| reflect.TypeOf() | 动态获取输入参数接口中的值的类型，如果为空则返回nil <- 注意是nil |

```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	// 定义一个Enum类型
	type Enum float32

	var name Enum = 3.1415926

	// TypeOf会返回目标数据的类型，比如int/float/struct/指针等
	reflectType := reflect.TypeOf(name)

	// valueOf返回目标数据的的值，比如上文的 3.1415926
	reflectValue := reflect.ValueOf(name)

	fmt.Println("类型: ", reflectType)
	fmt.Println("类型的名称: ", reflectType.Name())
	fmt.Println("类型的种类: ", reflectType.Kind())
	fmt.Println("变量值: ", reflectValue)
	fmt.Println("变量值的种类: ", reflectValue.Kind())
}

```

- 变量类型是指针与指针指向的元素：需要使用Elem方法。

| 方法 | 说明 |
| --- | --- |
| Field(i int) StructField | 根据索引返回索引对应的结构体字段的信息，当值不是结构体或索引超界时发生宕机 |
| NumField() int | 返回结构体成员字段数量，当类型不是结构体或索引超界时发生宕机 |
| FieldByName(name string) (StructField, bool) | 根据给定字符串返回字符串对应的结构体字段的信息，没有找到时 bool 返回 false，当类型不是结构体或索引超界时发生宕机 |
| FieldByIndex(index []int) StructField | 多层成员访问时，根据 []int 提供的每个结构体的字段索引，返回字段的信息，没有找到时返回零值。当类型不是结构体或索引超界时发生宕机 |
| FieldByNameFunc(match func(string) bool) (StructField,bool) | 根据匹配函数匹配需要的字段，当值不是结构体或索引超界时发生宕机 |

```go
package main
import (
	"fmt"
	"reflect"
)
func main() {
	// 声明一个空结构体
	type cat struct {
	}
	// 创建cat的实例
	ins := &cat{}
	// 获取结构体实例的反射类型对象
	typeOfCat := reflect.TypeOf(ins)
	// 显示反射类型对象的名称和种类
	fmt.Printf("name:'%v' kind:'%v'\n", typeOfCat.Name(), typeOfCat.Kind())
	// 取类型的元素
	typeOfCat = typeOfCat.Elem()
	// 显示反射类型对象的名称和种类
	fmt.Printf("element name: '%v', element kind: '%v'\n", typeOfCat.Name(), typeOfCat.Kind())
}
```

使用 reflect.Type 的 Field() 方法会返回 StructField 结构，这个结构描述结构体的成员信息：

```go
type StructField struct {
    Name string          // 字段名
    PkgPath string       // 字段路径
    Type      Type       // 字段反射类型对象
    Tag       StructTag  // 字段的结构体标签
    Offset    uintptr    // 字段在结构体中的相对偏移
    Index     []int      // Type.FieldByIndex中的返回的索引值
    Anonymous bool       // 是否为匿名字段
}
```

```go
package main
import (
    "fmt"
    "reflect"
)
func main() {
    // 声明一个空结构体
    type cat struct {
        Name string
        // 带有结构体tag的字段。tag：类似添加的注解，格式 `key1:"value1" key2:"value2"`
        Type int `json:"type" id:"100"`
    }
    // 创建cat的实例
    ins := cat{Name: "mimi", Type: 1}
    // 获取结构体实例的反射类型对象
    typeOfCat := reflect.TypeOf(ins)
    // 遍历结构体所有成员
    for i := 0; i < typeOfCat.NumField(); i++ {
        // 获取每个成员的结构体字段类型
        fieldType := typeOfCat.Field(i)
        // 输出成员名和tag
        fmt.Printf("name: %v  tag: '%v'\n", fieldType.Name, fieldType.Tag)
    }
    // 通过字段名, 找到字段类型信息
    if catType, ok := typeOfCat.FieldByName("Type"); ok {
        // 从tag中取出需要的tag
        fmt.Println(catType.Tag.Get("json"), catType.Tag.Get("id"))
    }
}
```

#### 反射三大定律

- 定律一：反射可以将“接口类型变量”转换为“反射类型对象” ：普通变量 -> 接口变量 -> 反射对象：
•

```go
func TypeOf(i interface{}) Type
func ValueOf(i interface{}) Value
```

##### 1.反射可以将“接口类型变量”转换为“反射类型对象

普通变量 -> 接口变量 -> 反射对象：

- 1.我们调用 reflect.TypeOf(name) 时，name被存储在一个空接口变量中,然后被传递过去；

![](/image/Golang03/Golang03_010.png)

- 2.接着**reflect.TypeOf** 或者 **ValueOf** 对空接口变量转换为 **reflect.Type** 或 **reflect.Value**。打个断点看看，如下图所示：

![](/image/Golang03/Golang03_011.png)

##### 2.反射可以将“反射类型对象”转换为“接口类型变量”

反射对象 -> 接口变量：使用的是Value 的Interface函数，是把实际的值赋值给空接口变量，它的声明如下：

```go
func (v Value) Interface() (i interface{})
```

```go
package main
import (
	"fmt"
	"reflect"
)
func main() {
	type MyInt int
	var x MyInt = 7
	v := reflect.ValueOf(x)
	// 通过 Interface 方法恢复其接口类型，然后再通过 接口断言获取值
	y := v.Interface().(MyInt)
	fmt.Printf("类型：%T\n", y)
	fmt.Println("值：", y)
}
```

##### 3.要修改“反射类型对象”其值必须是“可写的”

- 通过 CanSet 方法判断 reflect.Value 类型变量的“可写性”,看一下下面的例子：

```go
package main
import (
	"fmt"
	"reflect"
)
func main() {
	// 声明整型变量a并赋初值
	var a int = 1024
	// 获取变量a的反射值对象
	valueOfA := reflect.ValueOf(a)
	fmt.Println("可写性:", valueOfA.CanSet())
}
```

**可写性**，其实就是 **可以被寻址** 。

#### 通过反射修改变量的值

- 1.获取元素的地址，获取其反射值对象
- 2.获取其反射值对象的元素，修改值

```go
package main
import (
	"fmt"
	"reflect"
)
func main() {
	// 声明整型变量a并赋初值
	var a int = 1024
	// 获取变量a的反射值对象(a的地址)
	valueOfA := reflect.ValueOf(&a)
	// 取出a地址的元素(a的值)
	valueOfA = valueOfA.Elem()
	// 修改a的值为1
	valueOfA.SetInt(1)
	// 打印a的值
	fmt.Println(valueOfA.Int())
}
```

如果变量类型是结构体，需要考虑字段是否可以被导出。（首字符大写，小写会被隐蔽）

```go
package main
import (
	"fmt"
	"reflect"
)
func main() {
	type dog struct {
		LegCount int
	}
	// 获取dog实例地址的反射值对象
	valueOfDog := reflect.ValueOf(&dog{})
	// 取出dog实例地址的元素
	valueOfDog = valueOfDog.Elem()
	// 获取LegCount字段的值
	vLegCount := valueOfDog.FieldByName("LegCount")
	// 设置LegCount的值
	vLegCount.SetInt(4)
	fmt.Println(vLegCount.Int())
}
```

#### 方法

- 取元素、取地址及修改值的属性方法请参考下表：

| 方法名 | 备 注 |
| --- | --- |
| Elem() Value | 取值指向的元素值，类似于语言层*操作。当值类型不是指针或接口时发生宕 机，空指针时返回 nil 的 Value |
| Addr() Value | 对可寻址的值返回其地址，类似于语言层&操作。当值不可寻址时发生宕机 |
| CanAddr() bool | 表示值是否可寻址 |
| CanSet() bool | 返回值能否被修改。要求值可寻址且是导出的字段 |
| Set(x Value) | 将值设置为传入的反射值对象的值 |
- 值修改相关方法如下表所示：

| Set(x Value) | 将值设置为传入的反射值对象的值 |
| --- | --- |
| Setlnt(x int64) | 使用 int64 设置值。当值的类型不是 int、int8、int16、 int32、int64 时会发生宕机 |
| SetUint(x uint64) | 使用 uint64 设置值。当值的类型不是 uint、uint8、uint16、uint32、uint64 时会发生宕机 |
| SetFloat(x float64) | 使用 float64 设置值。当值的类型不是 float32、float64 时会发生宕机 |
| SetBool(x bool) | 使用 bool 设置值。当值的类型不是 bod 时会发生宕机 |
| SetBytes(x []byte) | 设置字节数组 []bytes值。当值的类型不是 []byte 时会发生宕机 |
| SetString(x string) | 设置字符串值。当值的类型不是 string 时会发生宕机 |

### 六、文件读写

使用语法如下所示：

```go
func OpenFile(name string, flag int, perm FileMode) (file *File, err error)
```

- name :文件的文件名，如果不是在当前路径下需要加上具体路径
- flag：文件的处理参数，表面上是int，实际上是枚举值。,如果要使用多个参数,需要用'|'连接
  - O_RDONLY：只读模式打开文件；
  - O_WRONLY：只写模式打开文件；
  - O_RDWR：读写模式打开文件；
  - O_APPEND：写操作时将数据附加到文件尾部（追加）；
  - O_CREATE：如果不存在将创建一个新文件；
  - O_EXCL：和 O_CREATE 配合使用，文件必须不存在，否则返回一个错误；
  - O_SYNC：当进行一系列写操作时，每次都要等待上次的 I/O 操作完成再进行；
  - O_TRUNC：如果可能，在打开时清空文件。
- perm：文件读/写/执行权限，同unix，有四位。
  - 第一位：
    - 4 ： set uid，设置使文件在执行阶段具有文件所有者的权限.
    - 2 ： set gid，目录被设置该位后, 任何用户在此目录下创建的文件都具有和该目录所属的组相同的组.
    - 1 ： sticky bit，防删除位.
  - 第二位：文件的所有者拥有的权限，如果同时拥有多种权限，把数字累加
    - 4：读
    - 2：写
    - 1：执行
  - 第三位：文件属组成员拥有的权限，如果同时拥有多种权限，把数字累加
    - 4：读
    - 2：写
    - 1：执行
  - 第四位：其他用户拥有的权限，如果同时拥有多种权限，把数字累加
    - 4：读
    - 2：写
    - 1：执行

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)
func main() {
	// 创建一个新文件，
	filePath := "golang.txt"
	// 设置创建和可写
	file, err := os.OpenFile(filePath, os.O_WRONLY|os.O_CREATE, 0666)
	if err != nil {
		fmt.Println("文件打开失败", err)
	}
	//及时关闭file句柄
	defer file.Close()
	//使用带缓存的 *Writer 写入文件，内容为 5 句 “Hello World”
	write := bufio.NewWriter(file)
	for i := 0; i < 5; i++ {
		write.WriteString("Hello World \n")
	}
	//Flush将缓存的文件真正写入到文件中
	write.Flush()
}
```

```go
package main
import (
	"bufio"
	"fmt"
	"io"
	"os"
)
func main() {
	filePath := "golang.txt"
	// 设置读写权限和追加模式
	file, err := os.OpenFile(filePath, os.O_RDWR|os.O_APPEND, 0666)
	if err != nil {
		fmt.Println("文件打开失败", err)
	}
	//及时关闭file句柄
	defer file.Close()
	//读原来文件的内容，并且显示在终端
	reader := bufio.NewReader(file)
	for {
		str, err := reader.ReadString('\n')
		if err == io.EOF {
			break
		}
		fmt.Print(str)
	}
	//写入文件时，使用带缓存的 *Writer
	write := bufio.NewWriter(file)
	for i := 0; i < 5; i++ {
		write.WriteString("Hello Golang \n")
	}
	//Flush将缓存的文件真正写入到文件中
	write.Flush()
}
```

#### 各种格式文件处理

##### JSON

JSON 文件内容一般是这样子：

```json
{"key1":"value1","key2":"value2","key3":["value3","value4","value5"]}
```

我们可以使用内置的 encoding/json 标准库去处理

```go
package main
import (
	"encoding/json"
	"fmt"
	"os"
)

type Website struct {
	Name   string `xml:"name,attr"`
	Url    string
	Course []string
}
func main() {
	// 1.写入文件
	// 定义了写个文件内容
	infoWrite := []Website{{"Golang", "https://golang.org/", []string{"http://www.baidu.com/"}},
		{"Java", "https://www.java.com/zh_CN/", []string{"http://www.google.com/java/"}}}
	// 创建文件
	filePtrWrite, err := os.Create("info.json")
	if err != nil {
		fmt.Println("文件创建失败", err.Error())
		return
	}
	// 创建Json编码器
	encoder := json.NewEncoder(filePtrWrite)
	err = encoder.Encode(infoWrite)
	if err != nil {
		fmt.Println("编码错误", err.Error())
	} else {
		fmt.Println("编码成功")
	}
	filePtrWrite.Close()

	// 2.读取文件
	filePtrRead, err := os.Open("./info.json")
	if err != nil {
		fmt.Println("文件打开失败 [Err:%s]", err.Error())
		return
	}
	defer filePtrRead.Close()
	var infoRead []Website
	// 创建json解码器
	decoder := json.NewDecoder(filePtrRead)
	err = decoder.Decode(&infoRead)
	if err != nil {
		fmt.Println("解码失败", err.Error())
	} else {
		fmt.Println("解码成功")
		fmt.Println(infoRead)
	}
}
```

##### XML

对于XML，我们可以使用 encoidng/xml 包

```go
package main
import (
	"encoding/xml"
	"fmt"
	"os"
)
type Website struct {
	Name   string `xml:"name,attr"`
	Url    string
	Course []string
}
func main() {
	// 1.写入文件
	// 定义写入信息
	infoWrite := Website{"Golang", "https://golang.org/", []string{"http://www.baidu.com/"}}
	f1, err := os.Create("./info.xml")
	if err != nil {
		fmt.Println("文件创建失败", err.Error())
		return
	}
	// 序列化到文件中
	encoder := xml.NewEncoder(f1)
	err = encoder.Encode(infoWrite)
	if err != nil {
		fmt.Println("编码错误：", err.Error())
		return
	} else {
		fmt.Println("编码成功")
	}
	f1.Close()

	// 2.读取文件
	// 打开xml文件
	f2, err := os.Open("./info.xml")
	if err != nil {
		fmt.Printf("文件打开失败：%v", err)
		return
	}
	defer f2.Close()
	infoRead := Website{}
	//创建 xml 解码器
	decoder := xml.NewDecoder(f2)
	err = decoder.Decode(&infoRead)
	if err != nil {
		fmt.Printf("解码失败：%v", err)
		return
	} else {
		fmt.Println("解码成功")
		fmt.Println(infoRead)
	}
}
```

##### Gob

Gob（即 Go binary 的缩写），Go语言自己以二进制形式序列化和反序列化程序数据的格式。

```go
package main
import (
	"encoding/gob"
	"fmt"
	"os"
)
func main() {
	// 1.写入文件
	info := map[string]string{
		"name":    "Golang",
		"website": "https://golang.org/",
	}
	name := "demo.gob"
	File1, _ := os.OpenFile(name, os.O_RDWR|os.O_CREATE, 0777)
	enc := gob.NewEncoder(File1)
	if err := enc.Encode(info); err != nil {
		fmt.Println(err)
	}
	File1.Close()
	
	// 2.读取文件
	var M map[string]string
	File2, _ := os.Open("demo.gob")
	D := gob.NewDecoder(File2)
	D.Decode(&M)
	fmt.Println(M)
}
```

##### bin

关于其他二进制文件，可以使用 encoding/binary处理。

语法如下：

```go
func Write(w io.Writer, order ByteOrder, data interface{}) error
func Read(r io.Reader, order ByteOrder, data interface{}) error
```

- w:可以读出字节流的数据源
- r:可以写入字节流的数据源
- order:指定写入/读取数据的字节序
    - binary.LittleEndian:小端模式,按照从低地址到高地址的顺序,存放据的低位字节到高位字节
    - binary.BigEndian:大端模式,按照从低地址到高地址的顺序,存放数据的高位字节到低位字节
- data:必须是定长值、定长值的切片、定长值的指针

```go
package main
import (
	"bytes"
	"encoding/binary"
	"fmt"
	"os"
)
type Website struct {
	Url int32
}

// 读取文件
func readNextBytes(file *os.File, number int) []byte {
	bytes := make([]byte, number)
	_, err := file.Read(bytes)
	if err != nil {
		fmt.Println("解码失败", err)
	}
	return bytes
}

func main() {
	// 1.写入文件
	file1, err := os.Create("output.bin")
	for i := 1; i <= 10; i++ {
		info := Website{
			int32(i),
		}
		if err != nil {
			fmt.Println("文件创建失败 ", err.Error())
			return
		}

		var binBuf bytes.Buffer
		binary.Write(&binBuf, binary.LittleEndian, info)
		b := binBuf.Bytes()
		_, err = file1.Write(b)
		if err != nil {
			fmt.Println("编码失败", err.Error())
			return
		}
	}
	fmt.Println("编码成功")
	file1.Close()

	// 2.读取文件
	// 打开文件
	file2, err := os.Open("output.bin")
	defer file2.Close()
	if err != nil {
		fmt.Println("文件打开失败", err.Error())
		return
	}
	m := Website{}
	for i := 1; i <= 10; i++ {
		data := readNextBytes(file2, 4)
		buffer := bytes.NewBuffer(data)
		err = binary.Read(buffer, binary.LittleEndian, &m)
		if err != nil {
			fmt.Println("二进制文件读取失败", err)
			return
		}
		fmt.Println("第", i, "个值为：", m)
	}
}
```

##### zip

```go
package main
import (
	"archive/zip"
	"bytes"
	"fmt"
	"io"
	"os"
)
func main() {
	// 1.压缩文件
	// 创建一个缓冲区用来保存压缩文件内容
	buf := new(bytes.Buffer)
	// 创建一个压缩文档
	w := zip.NewWriter(buf)
	// 将文件加入压缩文档
	var files = []struct {
		Name, Body string
	}{
		{"Golang.txt", "https://golang.org/"},
	}
	for _, file := range files {
		f, err := w.Create(file.Name)
		if err != nil {
			fmt.Println(err)
		}
		_, err = f.Write([]byte(file.Body))
		if err != nil {
			fmt.Println(err)
		}
	}
	// 关闭压缩文档
	err := w.Close()
	if err != nil {
		fmt.Println(err)
	}
	// 将压缩文档内容写入文件
	f, err := os.OpenFile("file.zip", os.O_CREATE|os.O_WRONLY, 0666)
	if err != nil {
		fmt.Println(err)
	}
	buf.WriteTo(f)

	// 2.解压文件
	// 打开一个zip格式文件
	r, err := zip.OpenReader("file.zip")
	if err != nil {
		fmt.Printf(err.Error())
	}
	defer r.Close()
	// 迭代压缩文件中的文件，打印出文件中的内容
	for _, f := range r.File {
		fmt.Printf("文件名: %s\n", f.Name)
		rc, err := f.Open()
		if err != nil {
			fmt.Printf(err.Error())
		}
		// 创建文件
		w, err := os.Create(f.Name)
		if err != nil {
			fmt.Printf(err.Error())
		}
		// 写入文件
		_, err = io.CopyN(w, rc, int64(f.UncompressedSize64))
		if err != nil {
			fmt.Printf(err.Error())
		}
		w.Close()
		rc.Close()
	}
}
```

##### tar

- 压缩的步骤如下：
    - 1.创建一个文件 x.tar，然后向 x.tar 写入 tar 头部信息；
    - 2.打开要被 tar 的文件，向 x.tar 写入头部信息，然后向 x.tar 写入文件信息；
    - 3.当有多个文件需要被 tar 时，重复第二步直到所有文件都被写入到 x.tar 中；
    - 4.关闭 x.tar，完成打包。

```go
package main
import (
	"archive/tar"
	"fmt"
	"io"
	"os"
)
func main() {
	f, err := os.Create("./output.tar") //创建一个 tar 文件
	if err != nil {
		fmt.Println(err)
		return
	}
	defer f.Close()
	tw := tar.NewWriter(f)
	defer tw.Close()
	fileinfo, err := os.Stat("Golang.txt") //获取文件相关信息
	if err != nil {
		fmt.Println(err)
	}
	hdr, err := tar.FileInfoHeader(fileinfo, "")
	if err != nil {
		fmt.Println(err)
	}
	err = tw.WriteHeader(hdr) //写入头文件信息
	if err != nil {
		fmt.Println(err)
	}
	f1, err := os.Open("Golang.txt")
	if err != nil {
		fmt.Println(err)
		return
	}
	m, err := io.Copy(tw, f1) //将Golang.txt文件中的信息写入压缩包中
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(m)
}
```

- 解压的步骤如下：
    - 1.打开文件 x.tar，然后从这个 tar 头部中循环读取存储在这个归档文件内的文件头信息；
    - 2.从这个文件头里读取文件名，以这个文件名创建文件，然后向这个文件里写入数据即可；

```go
package main
import (
	"archive/tar"
	"fmt"
	"io"
	"os"
)
func main() {
	f, err := os.Open("output.tar")
	if err != nil {
		fmt.Println("文件打开失败", err)
		return
	}
	defer f.Close()
	r := tar.NewReader(f)
	for hdr, err := r.Next(); err != io.EOF; hdr, err = r.Next() {
		if err != nil {
			fmt.Println(err)
			return
		}
		fileinfo := hdr.FileInfo()
		fmt.Println(fileinfo.Name())
		f, err := os.Create(fileinfo.Name()+"2")
		if err != nil {
			fmt.Println(err)
		}
		defer f.Close()
		_, err = io.Copy(f, r)
		if err != nil {
			fmt.Println(err)
		}
	}
}
```

#### 各种格式的速度以及大小对比

| 后缀 | 读取 | 写入 | 大小(KiB) | 读/写LOC | 格式 |
| --- | --- | --- | --- | --- | --- |
| .gob | 0.3 | 0.2 | 7948 | 21 + 11 =32 | Go二进制 |
| .gob.gz | 0.5 | 1.5 | 2589 |  |  |
| json | 4.5 | 2.2 | 16283 | 32+17 = 49 | JSON |
| .json.gz | 4.5 | 3.4 | 2678 |  |  |
| .xml | 6.7 | 1.2 | 18917 | 45 + 30 = 75 | XML |
| .xml.gz | 6.9 | 2.7 | 2730 |  |  |
| .txt | 1.9 | 1.0 | 12375 | 86 + 53 = 139 | 纯文本（UTF-8） |
| .txt.gz | 2.2 | 2.2 | 2514 |  |  |
| .bin | 1.7 | 3.5 | 7250 | 128 + 87 = 215 | 自定义二进制 |
| .bin.gz | 1.6 | 2.6 | 2400 |  |  |

More info: [Golang](http://c.biancheng.net/golang/)
