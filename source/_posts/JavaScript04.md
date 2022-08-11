---
title: JavaScript（四）ECMAScript
date: 2017-01-15 19:23:32
tags: [web,javascript]
copyright: true
password:
toc: true
---

**ECMAScript是一种由Ecma国际（前身为欧洲计算机制造商协会,英文名称是European Computer Manufacturers Association）通过ECMA-262标准化的脚本程序设计语言。这种语言在万维网上应用广泛，它往往被称为JavaScript或JScript，所以它可以理解为是JavaScript的一个标准，但实际上后两者是ECMA-262标准的实现和扩展。 **  本文章主要介绍 ECMAScript 的基本概念。

<!--more-->

## Quick Guide


### 一、结构

一个完整的 JavaScript 是由以下 3 个不同部分组成的：

- 核心（ECMAScript）： 是一个重要的标准, 描述了语法和基本对象。 
  - 语法
  - 类型
  - 语句
  - 关键字
  - 保留字
  - 运算符
  - 对象

- 文档对象模型（DOM）： HTML 和 XML 的应用程序接口（API）。DOM 将把整个页面规划成由节点层级构成的文档。HTML 或 XML 页面的每个部分都是一个节点的衍生物。 
  - DOM 视图 - 描述跟踪文档的各种视图（即 CSS 样式化之前和 CSS 样式化之后的文档）
  - DOM 事件 - 描述事件的接口
  - DOM 样式 - 描述处理基于 CSS 样式的接口
  - DOM 遍历和范围 - 描述遍历和操作文档树的接口

- 浏览器对象模型（BOM）： 对浏览器窗口进行访问和操作 
  - [Window 对象](https://www.w3school.com.cn/jsref/dom_obj_window.asp)
  - [Navigator 对象](https://www.w3school.com.cn/jsref/dom_obj_navigator.asp)
  - [Screen 对象](https://www.w3school.com.cn/jsref/dom_obj_screen.asp)
  - [History 对象](https://www.w3school.com.cn/jsref/dom_obj_history.asp)
  - [Location 对象](https://www.w3school.com.cn/jsref/dom_obj_location.asp)


### 二、ECMAScript的变量与类型

注意事项：
- 区分大小写
- 变量是弱类型的
- 每行结尾的分号可有可无
- 注释与 Java、C 和 PHP 语言的注释相同
    - 单行注释以双斜杠开头（//）
    - 多行注释以单斜杠和星号开头（/*），以星号和单斜杠结尾（*/）
- 括号表示代码块
-  ECMAScript 的解释程序遇到未声明过的标识符时，用该变量名创建一个全局变量，并将其初始化为指定的值。 

#### 2.1.变量声明

**使用 var 运算符声明变量。**

```javascript
// 声明变量
var test = "hi";
var test = "hi", age = 25;
// 变量并不一定要初始化
var test;
```

#### 2.2.命名变量

- 第一个字符必须是字母、下划线（_）或美元符号（$）
- 余下的字符可以是下划线、美元符号或任何字母或数字字符

```javascript
// Camel 标记法:首字母是小写的，接下来的字母都以大写字符开头
var myTestValue = 0, mySecondValue = "hi";
// Pascal 标记法:首字母是大写的，接下来的字母都以大写字符开头。
var MyTestValue = 0, MySecondValue = "hi";
// 匈牙利类型标记法:在以 Pascal 标记法命名的变量前附加一个小写字母（或小写字母序列），说明该变量的类型。
var iMyTestValue = 0, sMySecondValue = "hi";
```

#### 2.3.关键字

 关键字标识了 ECMAScript 语句的开头和/或结尾。根据规定，关键字是保留的，不能用作变量名或函数名。 

```javascript
break
case
catch
continue
default
delete
do
else
finally
for
function
if
in
instanceof
new
return
switch
this
throw
try
typeof
var
void
while
with
```

#### 2.4.保留字

 保留字在某种意思上是为将来的关键字而保留的单词。因此保留字不能被用作变量名或函数名。 

```javascript
abstract
boolean
byte
char
class
const
debugger
double
enum
export
extends
final
float
goto
implements
import
int
interface
long
native
package
private
protected
public
short
static
super
synchronized
throws
transient
volatile
```

#### 2.5.原始值

原始值：存储在栈（stack）中的简单数据段，也就是说，它们的值直接存储在变量访问的位置。

- Undefined： 当声明的变量未初始化时，该变量的默认值 
- Null： 表示尚未存在的对象 
- Boolean：  true 和 false 
- Number ： 
  - 32 位的整数
  - 64 位的浮点数
  - 八进制和十六进制
  - 特殊 ： Number.MAX_VALUE 、Number.MIN_VALUE ；Number.POSITIVE_INFINITY（ 生成的数大于Number.Max_VALUE ）和Number.NEGATIVE_INFINITY （ 生成的数值小于 Number.MIN_VALUE ）； NaN （ 类型 String、Boolean 转换失败 ）
- String 型 ：由双引号（"）或单引号（'）声明的。字符字面量


```javascript
// 类型检查
var sTemp = "test string";
alert (typeof sTemp);    //输出 "string"
alert (typeof 86);    //输出 "number"

// 所有整数都可以表示为八进制或十六进制的字面量，但所有数学运算返回的都是十进制结果。
var iNum = 070;  //070 等于十进制的 56
var iNum = 0x1f;  //0x1f 等于十进制的 31
// 对于浮点字面量的有趣之处在于，用它进行计算前，真正存储的是字符串。
var fNum = 5.0;
// 科学计数法
var fNum = 5.618e7

var sColor1 = "red";
var sColor2 = 'red';
```
#### 2.6.引用值

引用值：存储在堆（heap）中的对象，也就是说，存储在变量处的值是一个指针（point），指向存储对象的内存处。通常叫做类（class）。

```javascript
var o = new Object();
```

- 属性
    - constructor：对创建对象的函数的引用（指针）。对于 Object 对象，该指针指向原始的 Object() 函数。
    - Prototype：对该对象的对象原型的引用。对于所有的对象，它默认返回 Object 对象的一个实例。
- 方法
    - hasOwnProperty(property)：判断对象是否有某个特定的属性。必须用字符串指定该属性。
    - IsPrototypeOf(object)：判断该对象是否为另一个对象的原型。
    - PropertyIsEnumerable：判断给定的属性是否可以用 for...in 语句进行枚举。
    - ToString()：返回对象的原始字符串表示。
    - ValueOf()：返回最适合该对象的原始值。
- 类型
	- Boolean 对象 ：用于提供将布尔值转换成字符串
	- Number 对象 ：用于提供将布尔值转换成数字
		- toFixed() 方法 ：返回的是具有指定位数小数的数字的字符串
		- toExponential() 方法：返回的是用科学计数法表示的数字的字符串形式。
		- toPrecision() 方法：返回数字的预定形式或指数形式
	- String 对象
		- length 属性：符串中的字符个数
		- charAt(position)：获取字符串中的单个字符
		- charCodeAt(position)  ：获取字符串中的单个字符
		- concat()：把一个或多个字符串连接到 String 对象的原始值上
		- indexOf()：从字符串的开头（位置 0）开始检索字符串，返回位置值
		- lastIndexOf()：从字符串的结尾开始检索子串，返回位置值
		- localeCompare()：对字符串进行对比，入参大于对象返回1，等于返回0，小于返回-1
		- slice() ：截取字符串
		- substring()：截取字符串，会把负数作为0，把较小的数字作为起始位，较大的数字作为终止位。
		- toLowerCase()：小写
		- toLocaleLowerCase()：特定区域小写，建议是使用
		- toUpperCase()：大写
		- toLocaleUpperCase()：特定区域大写，建议是使用

#### 2.7.类型转换

```javascript
// 转换成字符串
var bFound = false;
alert(bFound.toString());	//输出 "false"
var iNum = 10;
alert(iNum.toString(2));	//输出 "1010"
alert(iNum.toString(8));	//输出 "12"
alert(iNum.toString(16));	//输出 "A"

// 转换成整数
var iNum1 = parseInt("12345red");	//返回 12345
var iNum1 = parseInt("0xA");	//返回 10
var iNum1 = parseInt("56.9");	//返回 56
var iNum1 = parseInt("red");	//返回 NaN

// 转换成浮点型
var fNum1 = parseFloat("12345red");	//返回 12345
var fNum2 = parseFloat("0xA");	//返回 NaN
var fNum3 = parseFloat("11.2");	//返回 11.2
var fNum4 = parseFloat("11.22.33");	//返回 11.22
var fNum5 = parseFloat("0102");	//返回 102
var fNum1 = parseFloat("red");	//返回 NaN

// 强转
// 转换成布尔型
var b1 = Boolean("");		//false - 空字符串
var b2 = Boolean("hello");		//true - 非空字符串
var b1 = Boolean(50);		//true - 非零数字
var b1 = Boolean(null);		//false - null
var b1 = Boolean(0);		//false - 零
var b1 = Boolean(new object());	//true - 对象

// 转换成数字
var iNum1 = Number(false)	//0
var iNum1 = Number(true)	//1
var iNum1 = Number(undefined)	//NaN
var iNum1 = Number(null)	//0
var iNum1 = Number("1.2")	//1.2
var iNum1 = Number("12")	//12
var iNum1 = Number("1.2.3")	//NaN
var iNum1 = Number(new object())	//NaN
var iNum1 = Number(50)	//50

// 转换成字符串
var s1 = String(null);	//"null"
var oNull = null;
var s2 = oNull.toString();	//会引发错误
```

#### 2.8.类型转换

```javascript
// instanceof 判断类型
var oStringObject = new String("hello world");
alert(oStringObject instanceof String);	//输出 "true"
```


### 三、ECMAScript的运算符

####  一元运算符

**一元运算符只有一个参数，即要操作的对象或值。** 

- delete:运算符删除对以前定义的对象属性或方法的引用。 

```javascript
var o = new Object;
o.name = "David";
alert(o.name);	//输出 "David"
delete o.name;
alert(o.name);	//输出 "undefined"
```

- void: 对任何值返回 undefined , 该运算符通常用于避免输出不应该输出的值 

```html
<a href="javascript:void(window.open('about:blank'))">Click me</a>
```

- 前增量/前减量运算符: 注意增量和减量运算符都发生在计算表达式之前

```javascript
var iNum = 10;
++iNum;
alert(iNum);	//输出 "11"
--iNum;
alert(iNum);	//输出 "10"
alert(--iNum);	//输出 "9"
alert(iNum);	//输出 "9"
```

- 后增量/后减量运算符:在计算过包含它们的表达式后才进行增量或减量运算的。

```javascript
var iNum = 10;
iNum++;
alert(iNum);	//输出 "11"
iNum--;
alert(iNum);	//输出 "10"
alert(iNum--);	//输出 "10"
alert(iNum);	//输出 "9"
```

- 一元加法和一元减法：对数字无任何影响，会把字符串转换成数字

```javascript
var sNum = "20";
alert(typeof sNum);	//输出 "string"
var iNum = +sNum;
alert(typeof iNum);	//输出 "number"

var sNum = "20";
alert(typeof sNum);	//输出 "string"
var iNum = -sNum;
alert(iNum);		//输出 "-20"
alert(typeof iNum);	//输出 "number"
```

####  位运算符

在数字底层（即表示数字的 32 个数位）进行操作的。


ECMAScript 整数有两种类型，即有符号整数（允许用正数和负数）和无符号整数（只允许用正数）。

![](/image/JavaScript04/ct_js_integer_binary_signed_32bits.png)

**注意：所有整数字面量都默认存储为有符号整数。只有 ECMAScript 的位运算符才能创建无符号整数。**

- NOT：由否定号（~）表示
    - 把运算数转换成 32 位数字
    - 把二进制数转换成它的二进制反码
    - 把二进制数转换成浮点数
- AND：由和号（&）表示
- OR：由符号（|）表示
- XOR： 由符号（^）表示，当只有一个数位存放的是 1 时，它才返回 1。
- 左移运算：由两个小于号表示（<<），数字中的所有数位向左移动指定的数量。
- 有符号右移运算：由两个大于号表示（>>），把 32 位数字中的所有数位整体右移，同时保留该数的符号（正号或负号）。负数（正数求反+1；带符号位移，左侧空位补1，-1求反，补充符号信息）
- 无符号右移运算：由三个大于号（>>>）表示，它将无符号 32 位数的所有数位整体右移。

####  逻辑运算符

逻辑运算符有三种：
* NOT：！表示
* AND：&& 表示
* OR：|| 表示

| 参数类型  | 结果                                                    |
| :-------- | :------------------------------------------------------ |
| Undefined | false                                                   |
| Null      | false                                                   |
| Boolean   | 结果等于输入的参数（不转换）                            |
| Number    | 如果参数为 +0, -0 或 NaN，则结果为 false；否则为 true。 |
| String    | 如果参数为空字符串，则结果为 false；否则为 true。       |
| Object    | true                                                    |


#### 乘性运算符

* 乘法运算符：由星号（*）表示，用于两数相乘。
* 除法运算符：由斜杠（/）表示，用第二个运算数除第一个运算数：
* 取模（余数）运算符：由百分号（%）表示
	* 如果被除数是 无穷大的数，或除数是 0，结果为 NaN。
	* 无穷大的数 被 无穷大的数 除，结果为 NaN。
	* 如果除数是无穷大的数，结果为被除数。
	* 如果被除数为 0，结果为 0。 	

#### 加性运算符

- 加法运算符：由加号（+）表示
    - 某个运算数是 NaN，那么结果为 NaN。
    - -Infinity 加 -Infinity，结果为 -Infinity。
    - Infinity 加 -Infinity，结果为 NaN。
    - +0 加 +0，结果为 +0。
    - -0 加 +0，结果为 +0。
    - -0 加 -0，结果为 -0。
    - 如果两个运算数都是字符串，把第二个字符串连接到第一个上。
    - 如果只有一个运算数是字符串，把另一个运算数转换成字符串，结果是两个字符串连接成的字符串。
- 减法运算符：由加号（-）表示
    - 某个运算数是 NaN，那么结果为 NaN。
    - Infinity 减 Infinity，结果为 NaN。
    - -Infinity 减 -Infinity，结果为 NaN。
    - Infinity 减 -Infinity，结果为 Infinity。
    - -Infinity 减 Infinity，结果为 -Infinity。
    - +0 减 +0，结果为 +0。
    - -0 减 -0，结果为 -0。
    - +0 减 -0，结果为 +0。
    - 某个运算符不是数字，那么结果为 NaN。

#### 关系运算符

关系运算符小于、大于、小于等于和大于等于执行的是两个数的比较运算，每个关系运算符都返回一个布尔值。

- 字符串相互比较：从左到右开始比较 字符串的ASCII大小
- 字符串和数字比较：把字符串转换成数字再比较大小，如果非数字字符串会转换为NaN，包含NaN结果为false
  

#### 等性运算符

等号和非等号用于处理原始值，全等号和非全等号用于处理对象。
- 等号：由双等号（==）表示，当且仅当两个运算数相等时，它返回 true。
- 非等号：由感叹号加等号（!=）表示，当且仅当两个运算数不相等时，它返回 true。

为确定两个运算数是否相等，这两个运算符都会进行类型转换。执行类型转换的规则如下：
- 如果一个运算数是 Boolean 值，在检查相等性之前，把它转换成数字值。false 转换成 0，true 为 1。
- 如果一个运算数是字符串，另一个是数字，在检查相等性之前，要尝试把字符串转换成数字。
- 如果一个运算数是对象，另一个是字符串，在检查相等性之前，要尝试把对象转换成字符串。
- 如果一个运算数是对象，另一个是数字，在检查相等性之前，要尝试把对象转换成数字


在比较时，该运算符还遵守下列规则：
- 值 null 和 undefined 相等。
- 在检查相等性时，不能把 null 和 undefined 转换成其他值。
- 如果某个运算数是 NaN，等号将返回 false，非等号将返回 true。
- 如果两个运算数都是对象，那么比较的是它们的引用值。如果两个运算数指向同一对象，那么等号返回 true，否则两个运算数不等。

- 全等号：由三个等号表示（===），只有在无需类型转换运算数就相等的情况下，才返回 true。
- 非全等号：由感叹号加两个等号（!==）表示，只有在无需类型转换运算数不相等的情况下，才返回 true。

#### 条件运算符

```javascript
variable = boolean_expression ? true_value : false_value;
```

该表达式主要是根据 *boolean_expression* 的计算结果有条件地为变量赋值。如果 *Boolean_expression* 为 true，就把 *true_value* 赋给变量；如果它是 false，就把 *false_value* 赋给变量。 

#### 赋值运算符

赋值运算符由等号（=）实现，只是把等号右边的值赋予等号左边的变量。 

- 简单赋值 (=)
- 乘法/赋值（*=）
- 除法/赋值（/=）
- 取模/赋值（%=）
- 加法/赋值（+=）
- 减法/赋值（-=）
- 左移/赋值（<<=）
- 有符号右移/赋值（>>=）
- 无符号右移/赋值（>>>=）

#### 逗号运算符

用逗号运算符可以在一条语句中执行多个运算。

```javascript
var iNum1 = 1, iNum = 2, iNum3 = 3;
```

### 四、ECMAScript的语句

#### if 语句

```javascript
// 如果条件计算结果为 true，则执行 statement1；如果条件计算结果为 false，则执行 statement2。
if (condition) statement1 else statement2;
// 如果 condition1 计算结果为 true，则执行 statement1；如果 condition1 计算结果为 false且 condition2条件为 true，则执行 statement2,否则执行 statement3。
if (condition1) statement1 else if (condition2) statement2 else statement3;
```

*condition* 可以是任何表达式，计算的结果甚至不必是真正的 boolean 值，ECMAScript 会把它转换成 boolean 值。 

#### 迭代语句

迭代语句又叫循环语句，声明一组要反复执行的命令，直到满足某些条件为止。

- do-while 语句:后测试循环，即退出条件在执行循环内部的代码之后计算。这意味着在计算表达式之前，至少会执行循环主体一次。

```javascript
do {statement} while (expression);
```
- while 语句:前测试循环。这意味着退出条件是在执行循环内部的代码之前计算的。因此，循环主体可能根本不被执行。

```javascript
while (expression) statement
```



-  for 语句:前测试循环，而且在进入循环之前，能够初始化变量，并定义循环后要执行的代码。 

```javascript
for (initialization; expression; post-loop-expression) statement
```

 **注意：post-loop-expression 之后不能写分号，否则无法运行。 ** 

- for 语句是严格的迭代语句，用于枚举对象的属性。

```javascript
for (property in expression) statement
```

#### 标签语句

 用下列语句给语句加标签，以便以后调用： 

```
label : statement
```

配合 break 或 continue 语句使用。 



####  break 和 continue 语句

- break 语句: 可以立即退出循环，阻止再次反复执行任何代码。
- continue 语句: 只是退出当前循环，根据控制表达式还允许继续进行下一次循环。

break 语句和 continue 语句都可以与有标签的语句联合使用，返回代码中的特定位置。

```javascript
var iNum = 0;

outermost:
for (var i=0; i<10; i++) {
  for (var j=0; j<10; j++) {
    if (i == 5 && j == 5) {
    break outermost;
  }
  iNum++;
  }
}

alert(iNum);	//输出 "55"

iNum = 0;

outermost:
for (var i=0; i<10; i++) {
  for (var j=0; j<10; j++) {
    if (i == 5 && j == 5) {
    continue outermost;
  }
  iNum++;
  }
}

alert(iNum);	//输出 "95"
```

#### with 语句

 with 语句:用于设置代码在特定对象中的作用域。 

```javascript
with (expression) statement
var sMessage = "hello";
with(sMessage) {
  alert(toUpperCase());	//输出 "HELLO"
}
```

 **提示：**with 语句是运行缓慢的代码块，尤其是在已设置了属性值时。大多数情况下，如果可能，最好避免使用它。 



#### switch 语句

 switch 语句是 if 语句的兄弟语句。 

```javascript
switch (expression)
  case value: statement;
    break;
  case value: statement;
    break;
  case value: statement;
    break;
  case value: statement;
    break;
...
  case value: statement;
    break;
  default: statement;
```

### 五、ECMAScript 函数

 函数的基本语法是这样的： 

```javascript
function functionName(arg0, arg1, ... argN) {
  statements // 可以return 返回值
}
```

调用函数:通过其名字加上括号中的参数进行调用，如果有多个参数。

```javascript
functionName(arg0, arg1, ... argN)
```



 特殊对象 arguments，开发者*无需明确指出参数名*，就能访问它们。 

```javascript
// 例如，在函数 sayHi() 中，第一个参数是 message。用 arguments[0] 也可以访问这个值，即第一个参数的值（第一个参数位于位置 0，第二个参数位于位置 1，依此类推）。
function sayHi() {
  if (arguments[0] == "bye") {
    return;
  }
	// 检测参数个数
	alert(arguments.length);
  alert(arguments[0]);
}

// 用 arguments 对象判断传递给函数的参数个数，即可模拟函数重载：
function doAdd() {
  if(arguments.length == 1) {
    alert(arguments[0] + 5);
  } else if(arguments.length == 2) {
    alert(arguments[0] + arguments[1]);
  }
}

doAdd(10);	//输出 "15"
doAdd(40, 20);	//输出 "60"
```

Function 对象（类）

```javascript

var function_name = new function(arg1, arg2, ..., argN, function_body)
// 输入参数个数
function_name.length
```

闭包，指的是词法表示包括不被计算的变量的函数，也就是说，函数可以使用函数之外定义的变量。

```javascript
// 简单
var sMessage = "hello world";

function sayHelloWorld() {
  alert(sMessage);
}

sayHelloWorld();

var iBaseNum = 10;

function addNum(iNum1, iNum2) {
  function doAdd() {
    return iNum1 + iNum2 + iBaseNum;
  }
  return doAdd();
}
```

### 六、对象

#### 面向对象术语

- 对象： 属性的无序集合，每个属性存放一个原始值、对象或函数 
- 类： 对象的抽象化。不仅要定义对象的接口（interface）（开发者访问的属性和方法），还要定义对象的内部工作（使属性和方法发挥作用的代码）。
- 实例： 使用类创建对象时，生成的对象叫作类的实例（instance）

基本能力：
- 封装 - 把相关的信息（无论数据或方法）存储在对象中的能力
- 聚集 - 把一个对象存储在另一个对象内的能力
- 继承 - 由另一个类（或多个类）得来类的属性和方法的能力
- 多态 - 编写能以多种方法运行的函数或方法的能力

对象的构成：
对象由特性（attribute）构成，特性可以是原始值，也可以是引用值。如果特性存放的是函数，它将被看作对象的方法（method），否则该特性被看作对象的属性（property）。

#### 对象应用
对象的创建和销毁都在 JavaScript 执行过程中发生，理解这种范式的含义对理解整个语言至关重要。

- 声明和实例化

```javascript
var oObject = new Object();
var oStringObject = new String();
```

- 对象废除
  ECMAScript 拥有垃圾回收程序（garbage collection routine）,把对象的所有引用都设置为 null，可以强制性地废除对象。

```javascript
var oObject = new Object;
// do something with the object here
oObject = null;
```

- 早绑定和晚绑定
所谓绑定（binding），即把对象的接口与对象实例结合在一起的方法。

早绑定（early binding 静态语言）是指在实例化对象之前定义它的属性和方法，这样编译器或解释程序就能够提前转换机器代码。

晚绑定（late binding 动态语言）指的是编译器或解释程序在运行前，不知道对象的类型。


#### 对象类型

- 本地对象( 引用类型 ):独立于宿主环境的 ECMAScript 实现提供的对象
    - Object
    - Function
    - Array
    - String
    - Boolean
    - Number
    - Date
    - RegExp
    - Error
    - EvalError
    - RangeError
    - ReferenceError
    - SyntaxError
    - TypeError
    - URIError
- 内置对象:由 ECMAScript 实现提供的、独立于宿主环境的所有对象
	- Global  
	- Math  
- 宿主对象
    - BOM 
    - DOM 

#### 对象作用域

ECMAScript 只有公用作用域,由于缺少私有作用域，开发者确定了一个规约，说明哪些属性和方法应该被看做私有的。这种规约规定在属性前后加下划线.

```javascript
obj._color_ = "blue";
```

```javascript
// 关键字 this 总是指向调用该方法的对象
var oCar = new Object;
oCar.color = "red";
oCar.showColor = function() {
  alert(this.color);
};

oCar.showColor();		//输出 "red"
```

#### 定义类或对象

- 工厂方式

```javascript
// 创造了能创建并返回特定类型的对象的工厂函数（factory function）。
function createCar() {
var oTempCar = new Object;
oTempCar.color = "blue";
oTempCar.doors = 4;
oTempCar.mpg = 25;
oTempCar.showColor = function() {
alert(this.color);
};
return oTempCar;
}

var oCar1 = createCar();
var oCar2 = createCar();
```
- 构造函数方式

```javascript
// 名字的首字母大写，以使它与首字母通常是小写的变量名分开,使用 this 关键字。使用 new 运算符构造函数时，在执行第一行代码前先创建一个对象，只有用 this 才能访问该对象。
function Car(sColor,iDoors,iMpg) {
this.color = sColor;
this.doors = iDoors;
this.mpg = iMpg;
this.showColor = function() {
alert(this.color);
};
}

var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);
```
- 原型方式
  

```javascript
// 用空构造函数来设置类名。然后所有的属性和方法都被直接赋予 prototype 属性
function Car() {
}

Car.prototype.color = "blue";
Car.prototype.doors = 4;
Car.prototype.mpg = 25;
Car.prototype.showColor = function() {
  alert(this.color);
};

var oCar1 = new Car();
var oCar2 = new Car();

//不同的实例修改属性值相互影响
oCar1.drivers.push("Bill");

alert(oCar1.drivers);	//输出 "Mike,John,Bill"
alert(oCar2.drivers);	//输出 "Mike,John,Bill"
```

- 混合的构造函数/原型方式

```javascript
// 所有的非函数属性都在构造函数中创建，意味着又能够用构造函数的参数赋予属性默认值了。
function Car(sColor,iDoors,iMpg) {
this.color = sColor;
this.doors = iDoors;
this.mpg = iMpg;
this.drivers = new Array("Mike","John");
}

Car.prototype.showColor = function() {
alert(this.color);
};

var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);

oCar1.drivers.push("Bill");

alert(oCar1.drivers);	//输出 "Mike,John,Bill"
alert(oCar2.drivers);	//输出 "Mike,John"
```

- 动态原型方法
```javascript
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.drivers = new Array("Mike","John");
  
  if (typeof Car._initialized == "undefined") {
    Car.prototype.showColor = function() {
      alert(this.color);
    };
	
    Car._initialized = true;
  }
}
```

- 混合工厂方式

```javascript
function Car() {
var oTempCar = new Object;
oTempCar.color = "blue";
oTempCar.doors = 4;
oTempCar.mpg = 25;
oTempCar.showColor = function() {
alert(this.color);
};

return oTempCar;
}
var car = new Car();
```

#### 修改对象

- 创建新方法

```javascript
// 通过已有的方法创建新方法
Number.prototype.toHexString = function() {
  return this.toString(16);
};
var iNum = 15;
alert(iNum.toHexString());		//输出 "F"

// 重命名已有方法
Array.prototype.enqueue = function(vItem) {
  this.push(vItem);
};

Array.prototype.dequeue = function() {
  return this.shift();
};

// 添加与已有方法无关的方法
Array.prototype.indexOf = function (vItem) {
  for (var i=0; i<this.length; i++) {
    if (vItem == this[i]) {
	  return i;
	}
  }

  return -1;
}
var aColors = new Array("red","green","blue");
alert(aColors.indexOf("green"));	//输出 "1"

// 为本地对象添加新方法
Object.prototype.showValue = function () {
  alert(this.valueOf());
};

var str = "hello";
var iNum = 25;
str.showValue();		//输出 "hello"
iNum.showValue();		//输出 "25"

// 重定义已有方法
Function.prototype.toString = function() {
  return "Function code hidden";
}
function sayHi() {
  alert("hi");
}

alert(sayHi.toString());	//输出 "Function code hidden"
```

### 七、继承机制实例

#### 对象冒充

```javascript
// 构造函数使用 this 关键字给所有属性和方法赋值（即采用类声明的构造函数方式）。
function ClassA(sColor) {
    this.color = sColor;
    this.sayColor = function () {
        alert(this.color);
    };
}
function ClassB(sColor, sName) {
    this.newMethod = ClassA;
    this.newMethod(sColor);
    delete this.newMethod;

    this.name = sName;
    this.sayName = function () {
        alert(this.name);
    };
}
```
#### call()

```javascript
// 与经典的对象冒充方法最相似的方法。它的第一个参数用作 this 的对象。其他参数都直接传递给函数自身。
function ClassB(sColor, sName) {
    //this.newMethod = ClassA;
    //this.newMethod(color);
    //delete this.newMethod;
    ClassA.call(this, sColor);

    this.name = sName;
    this.sayName = function () {
        alert(this.name);
    };
}
```

### apply()

```javascript
// 有两个参数，用作 this 的对象和要传递给函数的参数的数组
function ClassB(sColor, sName) {
    //this.newMethod = ClassA;
    //this.newMethod(color);
    //delete this.newMethod;
    ClassA.apply(this, new Array(sColor)); // 或 ClassA.apply(this, arguments);

    this.name = sName;
    this.sayName = function () {
        alert(this.name);
    };
}
```

#### 原型链

```javascript
function ClassA() {
}

ClassA.prototype.color = "blue";
ClassA.prototype.sayColor = function () {
    alert(this.color);
};

function ClassB() {
}

ClassB.prototype = new ClassA();

ClassB.prototype.name = "";
ClassB.prototype.sayName = function () {
    alert(this.name);
};

var objA = new ClassA();
var objB = new ClassB();
objA.color = "blue";
objB.color = "red";
objB.name = "John";
objA.sayColor();
objB.sayColor();
objB.sayName();
```

#### 混合方式

```javascript
function ClassA(sColor) {
    this.color = sColor;
}

ClassA.prototype.sayColor = function () {
    alert(this.color);
};

function ClassB(sColor, sName) {
    ClassA.call(this, sColor);
    this.name = sName;
}

ClassB.prototype = new ClassA();

ClassB.prototype.sayName = function () {
    alert(this.name);
};
var objA = new ClassA("blue");
var objB = new ClassB("red", "John");
objA.sayColor();	//输出 "blue"
objB.sayColor();	//输出 "red"
objB.sayName();	//输出 "John"
```

More info: [ECMAScript](https://www.w3school.com.cn/js/pro_js_operators_boolean.asp) 