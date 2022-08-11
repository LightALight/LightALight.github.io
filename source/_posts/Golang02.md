---
title: Golang（二）Go语言的基本语法(上)
date: 2021-03-15 22:23:32
tags: [golang]
copyright: true
password:
toc: true
---

　　本文章主要介绍 Golang 的基本语法。

<!--more-->

## Quick Guide

### 一、变量

#### 类型

- 基本
  - 布尔型
  - 数值
    - 整型
    - 浮点
    - 复数
  - 字符串
- 派生
  - 指针
  - 数值
  - 结构
  - 管道
  - 函数
  - 切片

#### 声明

##### 定义

```go
// 标准格式
var 变量名(命名规则遵循骆驼命名法,例如:aBit) 变量类型

// 批量格式
var (
    a int
    b string
    c []float32
    d func() bool
    e struct {
        x int
    }
)
```

##### 样例

```go
// c++
int* a,b; //a 是指针而 b 不是

// go
var a, b *int //a b 都是指针
```

##### 简短格式

- 定义变量,同时显式初始化
- 不能提供数据类型
- 只能用在函数内部

```go
名字 := 表达式
```

```go
package main    // 声明 main 包
import (
    "fmt"       // 导入 fmt 包，打印字符串是需要用到
)
func main() {   // 声明 main 主函数
	i, j := 0, 1
    fmt.Println(i,j) // 打印 Hello World!
}
```

##### 匿名变量

匿名变量是一个下画线"_"(空白标识符),仅用于声明,不能存储值.

```go
package main    // 声明 main 包
import (
    "fmt"       // 导入 fmt 包，打印字符串是需要用到
)

func GetData() (int, int) {
    return 100, 200
}
func main(){
    a, _ := GetData()
    _, b := GetData()
    fmt.Println(a, b)
}
```

##### 变量同时赋值

```go
package main    // 声明 main 包
import (
    "fmt"       // 导入 fmt 包，打印字符串是需要用到
)

func main() {   // 声明 main 主函数
    var a int = 100
    var b int = 200
    b, a = a, b
    fmt.Println(a, b)
}
```

#### 变量的作用域

- 函数内定义的变量称为局部变量
- 函数外定义的变量称为全局变量
- 函数定义中的变量称为形式参数

```go
package main
import (
    "fmt"
)
//全局变量 a
var a int = 0

func sum(a, b int) int {
    num := a + b
    return num
}

func main() {
    //局部变量 a 和 b
    c,d := 3,4
    f := sum(c, d)
    fmt.Printf("%d\n", f)
}
```

#### 数据类型转换

- Go语言不存在隐式类型转换,所以类型转换都必须显式声明
- *只有相同底层类型的变量之间才可以进行转换（例如 int16 转换成 int32）.不同将引起编译错误（例如 bool 转换为 int）*

```go
// 类型 B 的值 = 类型 B(类型 A 的值)
valueOfTypeB = typeB(valueOfTypeA)
```

```go
package main
import (
        "fmt"
)
func main() {
        // 初始化一个32位整型值
        var a int32 = 1008600
        // 输出变量的十六进制形式和十进制值
        fmt.Printf("int32: 0x%x %d\n", a, a)
        // 将a变量数值转换为十六进制, 发生数值截断
        b := int16(a)
        // 输出变量的十六进制形式和十进制值
        fmt.Printf("int16: 0x%x %d\n", b, b)
}
```

- ****字符串和数值类型的相互转换****
  
    Go中的 strconv 包( Atoi()、Itia()、parse 系列函数、format 系列函数、append 系列函数等)为我们提供了字符串和基本数据类型之间的转换功能.
    
    ```go
    package main
    
    import (
    	"fmt"
    	"strconv"
    )
    
    func main() {
    	str1 := "10010"
    	str2 := "t"
        // 字符串转换数字
    	num1, err := strconv.Atoi(str1)
    	if err != nil {
    		fmt.Printf("%v 转换失败！", str1)
    	} else {
    		fmt.Printf("type:%T value:%#v\n", num1, num1)
    	}
        // 字符串转换数字
    	num2, err := strconv.Atoi(str2)
    	if err != nil {
    		fmt.Printf("%v 转换失败！", str2)
    	} else {
    		fmt.Printf("type:%T value:%#v\n", num2, num2)
    	}
        // 字符串转换布尔型
    	boo1, err := strconv.ParseBool(str1)
    	if err != nil {
    		fmt.Printf("str1: %v\n", err)
    	} else {
    		fmt.Println(boo1)
    	}
        // 字符串转换布尔型
    	boo2, err := strconv.ParseBool(str2)
    	if err != nil {
    		fmt.Printf("str2: %v\n", err)
    	} else {
    		fmt.Println(boo2)
    	}
    }
    ```
    

#### 特殊的变量

一个变量存储一个值的内存地址

- 声明指针变量

```go
var var_name var_type = var_value
var ptr *var_type
```

- 为指针变量赋值变量的存储地址

```go
ptr := &var_name
```

- 访问指针变量中指向地址的值

```go
*ptr
```

- *当一个指针被定义后没有分配到任何变量时,它的值为 nil*

```go
package main

import "fmt"

func main() {
   var a int= 10   /* 声明实际变量 */
   var ak *int  /* 1.声明指针变量 */

   ak = &a  /* 2.为指针变量赋值变量的存储地址 */

   fmt.Printf("a 变量的地址是: %x\n", &a  )

   /* 指针变量的存储地址 */
   fmt.Printf("ak 变量储存的指针地址: %x\n", ak )

   /* 3.使用指针访问值 */
   fmt.Printf("*ak 变量的值: %d\n", *ak )
}
```

#### 常量

Go语言中的常量使用关键字 const 定义，用于存储不会改变的数据，常量是在编译时被创建的，即使定义在函数内部也是如此，并且只能是布尔型、数字型（整数型、浮点型和复数）和字符串型。由于编译时的限制，定义常量的表达式必须为能被编译器求值的常量表达式。

```go
const pi = 3.14159 // 相当于 math.Pi 的近似值
```

###### iota 常量生成器

```go
type Weekday int
const (
    Sunday Weekday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
)
```

###### 无类型常量

- 常量并没有一个明确的基础类型
- 编译器为这些没有明确的基础类型的数字常量提供比基础类型更高精度的算术运算

#### 变量的生命周期

变量的生命周期指的是在程序运行期间变量有效存在的时间间隔。

- 函数内定义的变量称为局部变量:从声明语句直到该变量不再被引用为止
- 函数外定义的变量称为全局变量:程序的运行周期一致
- 函数定义中的变量称为形式参数:函数被调用的时候创建

```go
package main

import "fmt"
var num int // 全局变量

func main() {
    num = 2
	for t := 0; t < num; t += 1 {
		x := int(t) // t 形式参数 x 局部变量
		fmt.Printf("x: %d\n", x)
	}
}
```

#### 类型别名

```go
type TypeAlias = Type

// 将NewInt定义为int类型
type NewInt int
// 将int取一个别名叫IntAlias
type IntAlias = int

// 定义商标结构
type Brand struct {
}
// 为Brand定义一个别名FakeBrand
type FakeBrand = Brand
```

- TypeAlias 只是 Type 的别名，本质上 TypeAlias 与 Type 是同一个类型，

#### 关键字与标识符

##### 关键字

关键字即是被Go语言赋予了特殊含义的单词，也可以称为保留字。

| break | default  | func | interface | select |
| --- | --- | --- | --- | --- |
| case | defer | go | map | struct |
| chan | else | goto | package | switch |
| const | fallthrough | if | range | type |
| continue | for | import | return | var |

##### 标识符

标识符是指Go语言对各种变量、方法、函数等命名时使用的字符序列，标识符由若干个字母、下划线`_`
、和数字组成，且第一个字符必须是字母。通俗的讲就是凡可以自己定义的名称都可以叫做标识符。

- 由 26 个英文字母、0~9、`_`组成；
- 不能以数字开头，例如 var 1num int 是错误的；
- Go语言中严格区分大小写；
- 标识符不能包含空格；
- 不能以系统保留关键字作为标识符，比如 break，if 等等。

### 二、注释

**注释的定义及使用**

```go
//单行注释

/*
第一行注释
第二行注释
...
*/
```

### 三、语句

#### 条件语句

##### if

语法如下:

```jsx
if 布尔表达式 {
   /* 在布尔表达式为 true 时执行 */
}

if 布尔表达式 {
   /* 在布尔表达式为 true 时执行 */
}else{
   /* 在布尔表达式为 false 时执行 */
}

if 布尔表达式1 {
   /* 在布尔表达式1为 true 时执行 */
}else if 布尔表达式2{
   /* 在布尔表达式2为 true 时执行 */
}else{
   /* 在布尔表达式1 2都为 false 时执行 */
}
```

```go
package main

import "fmt"

func main() {
	if true {
		fmt.Printf("在布尔表达式为 true 时执行\n")
	}

	if false {
		fmt.Printf("在布尔表达式为 true 时执行\n")
	} else {
		fmt.Printf("在布尔表达式为 false 时执行\n")
	}

	if false {
		fmt.Printf("在布尔表达式1为 true 时执行\n")
	} else if false {
		fmt.Printf("在布尔表达式2为 true 时执行\n")
	} else {
		fmt.Printf("在布尔表达式1和2都为 false 时执行\n")
	}
}
```

***关键字if和左边的大括号{必须同一行,关键字else必须和右边的大括号}在同一行,这两条规则都是被编译器强制规定的。***

##### switch

switch 用于基于不同条件执行不同动作，每一个 case 最后自带 break 语句,匹配成功后就不会执行其他 case,如果需要执行后面的 case,可以使用 fallthrough.

语法如下:

```go
switch var {
    case val1:
    /* var 为 val1 时执行 */
    case val2:
    /* var 为 val2 时执行 */
    case val3,val4,val5:
    /* var 为 val3或val4或val5 时执行 */
    /* 你可以定义任意数量的 case */
    default://可选
    /* var 都不满足上面的值执行 */
}

switch {
    case 布尔表达式1:
    /* 在布尔表达式1为 true 时执行 */
    case 布尔表达式2:
    /* 在布尔表达式2为 true 时执行 */
    case 布尔表达式3,布尔表达式4,布尔表达式5:
    /* 在布尔表达式3或者4或者5为 true 时执行 */
    /* 你可以定义任意数量的 case */
    default://可选
    /* var 都不满足上面的条件执行 */
}
```

#### 循环语句

##### for

```go
for 控制变量赋初值; 循环控制条件; 控制变量增量或减量 { 
   /* 循环控制条件为 true 时执行 */
}

for {
   /* 无限循环执行 */
}

//类似while
for 循环控制条件 { 
   /* 循环控制条件为 true 时执行 */
}

for inedex,value:= range (字符串/数组/切片){ 
   /* 对字符串、数组、切片等进行迭代输出元素 */
}

package main

import "fmt"

func main() {
	sum := 0
	for i := 0; i <= 10; i++ {
		sum += i
	}
	fmt.Println(sum)
	for j := 10; j <= 0; j-- {
		sum += j
	}
	fmt.Println(sum)
	for sum <= 10 {
		sum += sum
	}
	fmt.Println(sum)
	for sum <= 10 {
		sum += sum
	}
	fmt.Println(sum)
	// for {
	// 	sum++ // 无限循环下去
	// }
	// fmt.Println(sum) // 无法输出
	strings := []string{"google", "alibaba"}
	for i, s := range strings {
		fmt.Println(i, s)
	}

	numbers := [5]int{5, 4, 3, 2, 1}
	for i, x := range numbers {
		fmt.Printf("第 %d 位的值 = %d\n", i, x)
	}
}
```

#### 控制语句

可以控制语句的执行过程.

- break:用于中断当前 for 循环或跳出 switch 语句
- continue:跳过当前循环剩余的语句,进行下一轮循环
- goto:将跳转到被标记的语句

```go
package main

import "fmt"

func main() {

	for i := 0; i <= 10; i++ {
		fmt.Println(i)
		if 1 == 1 {
			fmt.Println("this is break.")
			break
		}
	}
	for i := 0; i <= 10; i++ {
		fmt.Println(i)
		if 1 == 1 {
			continue
			fmt.Println("this is skip statement.")
		}
	}

	var i int = 0

LOOP:
	for i <= 10 {
		fmt.Println(i)
		if i == 5 {
			// 跳过迭代
			i += 1
			goto LOOP
		}
		fmt.Printf("i的值为 : %d\n", i)
		i++
	}
}
```

### 四、函数

#### 普通函数

- 函数声明:包括函数名、形式参数列表、返回值列表（可省略）以及函数体,语法如下:
  
    ```go
    func 函数名(形式参数列表)(返回值列表){
        函数体
    }
    ```
    
    - 形式参数列表:函数的参数名以及类型,这些参数作为局部变量,其值由参数调用者提供
    - 返回值列表:函数返回值的变量名以及类型,如果函数返回一个无名变量或者没有返回值,则返回值列表的括号是可以省略的
- 调用函数
  
    ```go
    返回值变量列表 = 函数名(参数列表)
    ```
    
    - 函数名：需要调用的函数名。
    - 参数列表：参数变量以逗号分隔，尾部无须以分号结尾。
    - 返回值变量列表：多个返回值使用逗号分隔。
    
    ```go
    package main
    
    import (
        "fmt"
    )
    
    func add(x int, y int) int { return x + y }
    func sub(x, y int) (z int) { z = x - y; return }
    func zero(x int, y int)    { fmt.Printf("0") }
    func zero(args ...int)    { fmt.Printf("0") }
    
    func main() {
    
        fmt.Printf("%v\n", add(2, 1)) // 不带有变量名的返回值
        fmt.Printf("%v\n", sub(2, 1)) // 带有变量名的返回值
        fmt.Printf("%T\n", zero)      // 没有返回值
    }
    ```
    

#### 匿名函数

- 声明 语法如下:
  
    ```go
    func(参数列表)(返回参数列表){
        函数体
    }
    调用
    ```
    
    - 在定义时调用匿名函数
    - 作为回调函数:把函数作为值保存到变量中,然后调用函数变量
    
    ```go
    package main
    
    import "fmt"
    
    func main() {
    
        // 在定义时调用匿名函数,传递参数为 10086
        func(phone int) {
            fmt.Println("hello", phone)
        }(10086)
    
        // 匿名将匿名函数体保存到f()中
        f := func(phone int) {
            fmt.Println("hello", phone)
        }
        // 使用f()调用
        f(10086)
    }
    ```
    
##### 引用了外部变量的匿名函数--闭包
    
```go
package main

import (
  "fmt"
)

func main() {

  // 准备一个字符串
  str := "hello world"
  // 创建一个匿名函数
  foo := func() {

    // 匿名函数中访问str
    str = "hello dude"
  }
  // 调用匿名函数
  foo()
  fmt.Printf(str)
}
```
    
#### 方法
    
一种作用 于特定类型变量 的函数 。这种特定类型变量叫做接收器（ Receiver ） 。
如果将特定类型理解为结构体或“类”时，接收器的概念就类似于其他语言中的 this 或 者 self。
在 Go 语言中，接收器的类型可以是任何类型，不仅仅是结构体，任何类型都可以拥有方法。
    
```go
func (variable_name variable_data_type) function_name() [return_type]{
    /* 函数体*/
}

package main

import (
  "fmt"
)

/* 定义结构体 */
type Circle struct {
  radius float64
}

//该 method 属于 Circle 类型对象中的方法
func (c Circle) getArea() float64 {
  //c.radius 即为 Circle 类型对象中的属性
  return 3.14 * c.radius * c.radius
}

func main() {
  var c1 Circle
  c1.radius = 10.00
  fmt.Println("圆的面积 = ", c1.getArea())
}
```
    
#### 可变参数
    
```go
func function_name(args ...variable_data_type) [return_type]{
    /* 函数体*/
}
package main

import (
  "fmt"
)

func myArgs(args ...int) {
  for _, arg := range args {
    fmt.Println(arg)
  }
}

func main() {
  myArgs(2, 3, 4)
}
```
    
#### 延迟执行语句--defer
    
将其后面跟随的语句进行延迟处理,在 defer 归属的函数即将返回时,将延迟处理的语句按 defer 的逆序执行

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Println("defer begin")
  // 将defer放入延迟调用栈
  defer fmt.Println(1)
  defer fmt.Println(2)
  // 最后一个放入, 位于栈顶, 最先调用
  defer fmt.Println(3)
  fmt.Println("defer end")
}
```
    


More info: [Golang](http://c.biancheng.net/golang/)
