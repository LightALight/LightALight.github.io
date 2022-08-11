---
title: JavaScript（一）JavaScript的基本知识(上)
date: 2016-10-15 19:23:32
tags: [web,javascript]
copyright: true
password:
toc: true
---

 **JavaScript 是世界上最流行的脚本语言， 是属于 HTML 和 Web 的编程语言。** 本文章主要介绍 JavaScript 的基本语法。

<!--more-->

## Quick Guide

JavaScript 是 web 开发者必学的三种语言之一：
- HTML 定义网页的内容
- CSS 规定网页的布局
- JavaScript 对网页行为进行编程

### 一、用途


- JavaScript 能够改变 HTML 内容

```html
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript 能做什么</h2>

<p id="demo">JavaScript 能够改变 HTML 内容。</p>

<button type="button" onclick='document.getElementById("demo").innerHTML = "Hello JavaScript!"'>点击我！</button>

</body>
</html>
```

- JavaScript 能够改变 HTML 属性
```html
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript 能做什么？</h2>

<p>JavaScript 能够改变 HTML 属性值。</p>

<p>在本例中，JavaScript 改变了图像的 src 属性值。</p>

<button onclick="document.getElementById('myImage').src='/i/eg_bulbon.gif'">开灯</button>

<img id="myImage" border="0" src="/i/eg_bulboff.gif" style="text-align:center;">

<button onclick="document.getElementById('myImage').src='/i/eg_bulboff.gif'">关灯</button>

</body>
</html>
```
- JavaScript 能够改变 HTML 样式
```html
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript 能够做什么</h2>

<p id="demo">JavaScript 能够改变 HTML 元素的样式。</p>

<button type="button" onclick="document.getElementById('demo').style.fontSize='35px'">
点击我！
</button>


</body>
</html> 
```
- JavaScript 能够隐藏 HTML 元素
```html
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript 能够做什么</h2>

<p id="demo">JavaScript 能够隐藏 HTML 元素。</p>

<button type="button" onclick="document.getElementById('demo').style.display='none'">
点击我！
</button>


</body>
</html>
```
- JavaScript 能够显示 HTML 元素
```html
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript 能够做什么</h2>

<p>JavaScript 能够显示隐藏的 HTML 元素。</p>

<p id="demo" style="display:none">Hello JavaScript!</p>

<button type="button" onclick="document.getElementById('demo').style.display='block'">
点击我！
</button>

</body>
</html>
```
### 二、使用

在 HTML 中， 脚本可被放置与 HTML 页面的 `<body>` 或 `<head>` 部分中 `<script>` 与 `</script>` 标签之间。

#### 内部引用

```html
<!DOCTYPE html>
<html>
<head>
<script>
function myFunction() {
    document.getElementById("demo").innerHTML = "段落被更改。";
}
</script>
</head>

<body>

<h1>一张网页</h1>
<p id="demo">一个段落</p>
<button type="button" onclick="myFunction()">试一试</button>

</body>
</html>
```

#### 外部引用

- 分离了 HTML 和代码

- 使 HTML 和 JavaScript 更易于阅读和维护

- 已缓存的 JavaScript 文件可加速页面加载

```javascript
// 外部myScript.js
function myFunction() {
   document.getElementById("demo").innerHTML = "段落被更改。";
}
```

```html
<script type="text/javascript" src="myScript.js"></script>
```



### 三、基本语法

#### 3.1.输出

- 使用 window.alert() 写入警告框
- 使用 document.write() 写入 HTML 输出
- 使用 innerHTML 写入 HTML 元素
- 使用 console.log() 写入浏览器控制台

```html
<!DOCTYPE html>
<html>
<body>
<h1>我的第一张网页</h1>
<p>我的第一个段落</p>
<p id="demo"></p>

<script>
 document.getElementById("demo").innerHTML = 5 + 6;
</script>

</body>
</html> 
```

```html
<!DOCTYPE html>
<html>
<body>
<h1>我的第一张网页</h1>
<p>我的第一个段落</p>
<p id="demo"></p>

<script>
 document.getElementById("demo").innerHTML = 5 + 6;
</script>

</body>
</html> 
```
```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>

<script>
window.alert(5 + 6);
</script>

</body>
</html> 
```
```html
<!DOCTYPE html>
<html>
<body>

<h1>我的第一张网页</h1>

<p>我的第一个段落</p>
<!-- 在 debugger 中选择 "Console"。然后再次点击运行按钮。 -->
<script>
console.log(5 + 6);
</script>

</body>
</html>
```

#### 3.2.语句

由 值、运算符、表达式、关键词和注释构成。
- 关键词：代码内部用于标识被执行的动作
- 值：字面量（具体的数据）和变量值（存储字面量的名称）
- 运算符：如算数运算符（+ - * /）
- 表达式：变量和运算符的组合，计算结果是值
- 注释：代码描述说明

```javascript
var x, y;	// 如何声明变量
x = 7; y = 8;	// 如何赋值
z = x + y;	// 如何计算值
```

关键词指的是保留的单词。保留词无法用作变量名。

| 关键词        | 描述                                              |
| :------------ | :------------------------------------------------ |
| break         | 终止 switch 或循环。                              |
| continue      | 跳出循环并在顶端开始。                            |
| debugger      | 停止执行 JavaScript，并调用调试函数（如果可用）。 |
| do ... while  | 执行语句块，并在条件为真时重复代码块。            |
| for           | 标记需被执行的语句块，只要条件为真。              |
| function      | 声明函数。                                        |
| if ... else   | 标记需被执行的语句块，根据某个条件。              |
| return        | 退出函数。                                        |
| switch        | 标记需被执行的语句块，根据不同的情况。            |
| try ... catch | 对语句块实现错误处理。                            |
| var           | 声明变量。                                        |


**注意:**

- 1.使用分号分隔语句
- 2.增加适当空格(符号之间或者代码块的缩进)提高可读性 
- 3.代码行控制在 80 个字符以内 
- 4.使用花括号包围代码块
- 5.双斜杠 // 或 /* 与 */ 之间的代码被视为注释

#### 3.3.标识符

标识符:有 变量 和 关键词。下面是命名规则：
- 名称可包含字母、数字、下划线和美元符号
- 名称必须以字母开头
- 名称也可以 $ 和 _ 开头（一般不会这么做）
- 名称对大小写敏感（y 和 Y 是不同的变量）
- 保留字（比如 JavaScript 的关键词）无法用作变量名称

#### 3.4.变量

存储数据值的容器，变量必须以唯一的名称的标识。

```javascript
// 声明未定义,值为undefined
var carName;

// 声明且定义
var carName = "porsche";
var person = "Bill Gates", carName = "porsche", price = 15000;

// 重复声明 
var carName = "porsche";
var carName; 
```

#### 3.5.数据类型

变量可用作不同类型
- 数据类型
    - [字符串值](#字符串值)
    - [数值](#数值)
    - [布尔值](#布尔值)
    - 不包含任何值
      - [undefined](#undefined)
      - null
    - function
- 对象类型
	- [object](#对象)
	- Date
	- Array

##### 字符串值

```javascript
// 字符串
var answer = "It's alright";             // 双引号内的单引号
var answer = "He is called 'Bill'";    // 双引号内的单引号
var answer = 'He is called "Bill"';    // 单引号内的双引号
var x = "中国是瓷器的故乡，因此 china 与\"China（中国）\"同名。"  // 转义字符\
var firstName = new String("Bill")   // 字符串对象

// 字符串的长度
var sln = answer.length; 

// 返回字符串中指定文本首次出现的索引
var str = "The full name of China is the People's Republic of China.";
var pos = str.indexOf("China");  
var pos = str.indexOf("China", 18);  // 18是起始位
var pos = str.search("locate"); // 支持正则

// 返回指定文本在字符串中最后一次出现的索引
var pos = str.lastIndexOf("China");
var pos = str.lastIndexOf("China", 15); // 15是起始位

// 截取字符串
var str = "Apple, Banana, Mango";
var res = str.slice(7,13);
var res = str.slice(-13,-7);
var res = str.slice(7);
var res = str.substring(7,13);  // 无法接受负的索引
var res = str.substr(7,6);  // 第二个参数规定被提取部分的长度

// 提取字符串字符
var str = "HELLO WORLD";
str.charAt(0);            // 返回 H
str.charCodeAt(0);         // 返回 unicode 编码 72

// 替换字符串,只替换首个匹配
var n1 = str.replace("Banana", "W3School");
var n2 = str.replace(/BANANA/i, "W3School"); //大小写不敏感的替换,正则不需要双引号

// 转换为大写和小写
var text2 = n1.toUpperCase();  // BANANA
var text2 = n1.toLowerCase();  // banana

//连接两个或多个字符串
var text = "Hello" + " " + "World!";
var text = "Hello".concat(" ","World!");

// 删除字符串两端的空白符
var str = "       Hello World!        ";
alert(str.trim());

// 属性访问
var str = "HELLO WORLD";
str[0];                   // 返回 H

// 把字符串转换为数组
var txt = "a,b,c,d,e";   // 字符串
txt.split(",");          // 用逗号分隔
```

##### 数值

```javascript
// 数值:64 位的浮点数 
var x1 = 34.00;     // 带小数点
var x2 = 34;        // 不带小数点
var y = 123e5;      // 12300000
var z = 123e-5;     // 0.00123
// 整数（不使用指数或科学计数法）会被精确到 15 位 
var x = 999999999999999;   // x 将是 999999999999999
var y = 9999999999999999;  // y 将是 10000000000000000
// 小数的最大数是 17 位，但是浮点的算数并不总是 100% 精准
var x = 0.2 + 0.1;         // x 将是 0.30000000000000004

// 把要给数值放入引号中，其余数值会被视作字符串并被级联。
var x = "Bill" + " " + "Gates";
var x = "8" + 3 + 5;
// 数字运算中（加法除外），将字符串转换为数字
var x = "100";
var y = "10";
var z = x / y;       // z 将是 10

// NaN 属于 JavaScript 保留词，指示某个数不是合法数。
var x = 100 / "Apple";  // x 将是 NaN（Not a Number）
isNaN(x);               // 返回 true，因为 x 不是数
var y = "5";
var z = x + y;         // z 将是 NaN5
typeof NaN;             // 返回 "number"
// Infinity （或 -Infinity）是 JavaScript 在计算数时超出最大可能数范围时返回的值。
var x =  2 / 0;          // x 将是 Infinity
var y = -2 / 0;          // y 将是 -Infinity
typeof Infinity;        // 返回 "number"
// 前缀为 0x 的数值常量解释为十六进制
var x = 0xFF;             // x 将是 255

// 数字对象
var a = new Number(123);   // typeof a 返回 object
var x = 500;   
var y = new Number(500); // (x == y) 为 true,因为 x 和 y 有相等的值(x === y) 为 false,类型不同
var z = new Number(500); // (y == z) 为 false,因为对象不可以比较

// 转换为字符串
var myNumber = 128;
myNumber.toString(16);     // 返回 80
myNumber.toString(8);      // 返回 200
myNumber.toString(2);      // 返回 10000000

// 返回字符串值，它包含已被四舍五入并使用指数计数法的数字。
var x = 9.656;
x.toExponential(2);     // 返回 9.66e+0
x.toExponential(4);     // 返回 9.6560e+0
x.toExponential(6);     // 返回 9.656000e+0

// 返回字符串值，它包含了指定位数小数的数字
var x = 9.656;
x.toFixed(0);           // 返回 10
x.toFixed(2);           // 返回 9.66
x.toFixed(4);           // 返回 9.6560
x.toFixed(6);           // 返回 9.656000

// 返回字符串值，它包含了指定长度的数字：
var x = 9.656;
x.toPrecision();        // 返回 9.656
x.toPrecision(2);       // 返回 9.7
x.toPrecision(4);       // 返回 9.656
x.toPrecision(6);       // 返回 9.65600

//  返回对象的原始值
var a = new Number(123);
a.valueOf();   // 从表达式 100 + 23 返回 123

// 转换为数字
Number("10");        // 返回 10
x = Number("10 20");        // 返回 NaN
Number(new Date("2019-04-15"));    // 返回 1506729600000

// 解析一段字符串并返回数值。允许空格。只返回首个数字：
parseInt("10 years");   // 返回 10
parseInt("years 10");   // 返回 NaN
parseFloat("10.33");     // 返回 10.33
parseFloat("10 years");  // 返回 10
parseFloat("10 20 30");  // 返回 10

// 数值属性
MAX_VALUE	// 返回 JavaScript 中可能的最大数。
MIN_VALUE	// 返回 JavaScript 中可能的最小数。
NEGATIVE_INFINITY	// 表示负的无穷大（溢出返回）。
NaN	// 表示非数字值（"Not-a-Number"）。
POSITIVE_INFINITY	// 表示无穷大（溢出返回）。
var x = Number.MAX_VALUE; // 数字属性不可用于变量
```

##### 布尔值

```javascript
// 布尔值
var x = true;
var y = false;

```

##### undefined

```javascript
// 空
var person;                  // 值是 undefined，类型是 undefined
person = undefined;          // 值是 undefined，类型是 undefined
var car = "";                // 值是 ""，类型是 "string"
var person = null;           // 值是 null，但是类型仍然是对象
typeof undefined              // undefined
typeof null                   // object
null === undefined            // false
null == undefined             // true 等值不等型
```

##### 对象

```javascript
// 数组:一种特殊类型的对象,使用数字索引
var array_name = [item1, item2, ...];
var cars = new Array("Saab", "Volvo", "BMW");
var cars = ["Porsche", "Volvo", "BMW"]; // 请不要最后一个元素之后写逗号（比如 "BMW",）。

var name = cars[0]; // Porsche 通过引用索引号（下标号）来引用某个数组元素
cars[0] = "Opel";  // 改变数组元素
cars.length;  // 返回数组的长度（数组元素的数目）

var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.push("Lemon");                // 向 fruits 添加一个新元素 (Lemon),x 的值是 5(返回新数组的长度)
fruits[fruits.length] = "Lemon";     // 向 fruits 添加一个新元素 (Lemon)
var x = fruits.pop(); // fruits 删除最后一个元素（"Mango"）,x 的值是 "Mango"
var x = fruits.shift();            // 从 fruits 删除第一个元素 "Banana",x 的值是 "Banana
delete fruits[0];           // 把 fruits 中的首个元素改为 undefined
fruits.unshift("Lemon");    // 向 fruits 添加新元素 "Lemon", 返回新数组的长度
var removed = fruits.splice(2, 2, "Lemon", "Kiwi");  // 从位置 2 开始删除 2 个元素 添加新元素 "Lemon,Kiwi", 返回删除元素

// 数组转换字符串
document.getElementById("demo").innerHTML = fruits.toString(); // Banana,Orange,Apple,Mango
document.getElementById("demo").innerHTML = fruits.join(" * "); // Banana * Orange * Apple * Mango
var myGirls = ["Emma", "Isabella"];
var myBoys = ["Jacob", "Michael", "Ethan"];
var myChildren = myGirls.concat(myBoys);  // Emma,Isabella,Jacob,Michael,Ethan
var arr1 = ["Cecilie", "Lone"];
var arr2 = ["Emil", "Tobias", "Linus"];
var arr3 = ["Robin", "Morgan"];
var myChildren = arr1.concat(arr2, arr3);   // 将arr1、arr2 与 arr3 连接在一起

// 切片新数组
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(3);  // Apple,Mango
var citrus = fruits.slice(1, 3); // Orange,Lemon

// 最大值
var arr = [1,2,3]
Math.max(1, 2, 3) // 不允许直接放入数组
Math.max.apply(null, arr)
Math.min(1, 2, 3) 
Math.min.apply(null, arr)

// 遍历数组
for (i = 0; i < cars.length; i++) {
     text += "<li>" + cars[i] + "</li>";
} 
text1 = "<ul>";
text2 = "<ul>";
text3 = "<ul>";
fruits.forEach(myFunction);

function myFunction(value, index, array) {
  text1 += "<li>" + value + "</li>"; // 项目值
  text2 += "<li>" + index + "</li>"; // 项目索引
  text3 += "<li>" + array + "</li>"; // 数组本身
}

// 以字母顺序对数组进行排序：
fruits.sort();            // 对 fruits 中的元素进行排序
fruits.reverse();         // 反转元素顺序
var points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return a - b}); // 数字也会当作字符串比较,需要用比值函数
points.sort(function(a, b){return 0.5 - Math.random()}); // 随机顺序排序数组

var numbers = [45, 4, 9, 16, 25];
// 对每个数组元素执行函数来创建新数组
var numbers2 = numbers.map(myFunction);
function myFunction(value, index, array) {
  return value * 2;
}
// 过滤,创建一个包含通过测试的数组元素的新数组
var over18 = numbers.filter(myFunction);
function myFunction(value, index, array) {
  return value > 18;
}
// 检查所有数组值是否通过测试
var allOver18 = numbers.every(myFunction); // True
function myFunction(value, index, array) {
  return value > 18;
}
// 检查所有数组值是否通过测试
var allOver18 = numbers.every(myFunction); // True
function myFunction(value, index, array) {
  return value > 18;
}
// 检查数组值是否有通过测试
var allOver18 = numbers.some(myFunction); // True
function myFunction(value, index, array) {
  return value > 18;
}
// 返回通过测试函数的第一个数组元素的值
var first = numbers.find(myFunction);
function myFunction(value, index, array) {
  return value > 18;
}
// 返回通过测试函数的第一个数组元素的索引
var first = numbers.findIndex(myFunction);
function myFunction(value, index, array) {
  return value > 18;
}
// 在数组中搜索元素值并返回其位置
var a = points.indexOf(100,0)  // a为1,第二个参数可选 是起始位,搜索到结尾
var a = fruits.lastIndexOf(100);  // a为1,第二个参数可选 是起始位,搜索到开头


// 递归
var sum = numbers.reduce(myFunction,100); // 100为初始值,可选填
var sum = numbers1.reduceRight(myFunction);  // 在数组中从右到左工作
function myFunction(total, value, index, array) {
  return total + value;  // total:总数（初始值/先前返回的值）
}

// 判断是否数组
Array.isArray(fruits);     // 返回 true
function isArray(x) {
    return x.constructor.toString().indexOf("Array") > -1;
} // 自定义
fruits instanceof Array     // 返回 true


// 日期,格式Thu Dec 03 2020 20:32:48 GMT+0800 (中国标准时间)
var d = new Date(); 
var d = new Date(year, month, day, hours, minutes, seconds, milliseconds)
var d = new Date(2018, 11);  // year month
var d = new Date(99, 11, 24); // 一位和两位数年份将被解释为 19xx 年
var d = new Date(2018, 11, 24); // year month day
var d = new Date(2018, 11, 24, 10); // year month day hours
var d = new Date("October 13, 2014 11:13:00");
new Date(milliseconds);
new Date(date string);


// 对象使用命名索引
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"};

typeof {name:'Bill', age:62} // 返回 "object"
typeof [1,2,3,4]             // 返回 "object" (数组也是对象)
typeof null                  // 返回 "object"
typeof function myFunc(){}   // 返回 "function"
// 访问对象属性
objectName.propertyName
objectName["propertyName"]
// 访问对象方法
objectName.methodName()
name = person.fullName; // 不使用 () 访问 fullName 方法，则将返回函数定义：
```


| 代码 | 结果       |
| :--- | :--------- |
| \b   | 退格键     |
| \f   | 换页       |
| \n   | 新行       |
| \r   | 回车       |
| \t   | 水平制表符 |
| \v   | 垂直制表符 |


##### 获取类型

- typeof
  - 使用 typeof 操作符来查看 JavaScript 变量的数据类型。
  - NaN 的数据类型是 number
  - 数组(Array)的数据类型是 object
  - 日期(Date)的数据类型为 object
  - null 的数据类型是 object
  - 未定义变量的数据类型为 undefined

```javascript
typeof "John"                 // 返回 string
typeof 3.14                   // 返回 number
typeof NaN                    // 返回 number
typeof false                  // 返回 boolean
typeof [ 1,2,3,4]              // 返回 object
typeof {name: 'John', age:34}  // 返回 object
typeof new Date()             // 返回 object
typeof function () {}         // 返回 function
typeof myCar                  // 返回 undefined (如果 myCar没有被实例化的话)
typeof null                   // 返回 object
```
如果对象是 JavaScript Array 或 JavaScript Date ，我们就无法通过 **typeof** 来判断他们的类型，因为都是 返回 Object。

- constructor

constructor 属性返回所有 JavaScript 变量的构造函数。

```javascript
"John".constructor                 // 返回函数 String()  { [native code] }
(3.14).constructor                 // 返回函数 Number()  { [native code] }
false.constructor                  // 返回函数 Boolean() { [native code] }
[1,2, 3,4].constructor              // 返回函数 Array()   { [native code] }
{name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
new Date().constructor             // 返回函数 Date()    { [native code] }
function() {}.constructor         // 返回函数 Function(){ [native code] }
```

##### 类型转换

JavaScript 变量可以转换为新变量或其他数据类型：
- 通过使用 JavaScript 函数
- 通过 JavaScript 自身自动转换

###### 转换为字符串

```javascript
// 将数字转换为字符串
String(x)         // 将变量 x 转换为字符串并返回
String(123)       // 将数字 123 转换为字符串并返回
String( 100+ 23)  // 将数字表达式转换为字符串并返回
x.toString()
(123).toString()
(100 + 23).toString()

// 将布尔值转换为字符串
String(false)        // 返回 "false"
String(true)         // 返回 "true"
false.toString()     // 返回 "false"
true.toString()      // 返回 "true"

// 将日期转换为字符串
String(Date())      // 返回 Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)

Date().toString()   // 返回 Thu Jul 17 2014 15:38:19 GMT+0200 (W. Europe Daylight Time)

```

###### 转换为数字

```javascript
//将字符串转换为数字

Number("3.14")    // 返回 3.14
Number(" ")       // 返回 0
Number("")        // 返回 0
Number("99 88")   // 返回 NaN

// 一元运算符 +
var y = "5";      // y 是一个字符串
var x = + y;      // x 是一个数字
var y = "John";   // y 是一个字符串
var x = + y;      // x 是一个数字 (NaN)

//将布尔值转换为数字
Number(false)     // 返回 0
Number(true)      // 返回 1

//将日期转换为数字
d = new Date();
Number(d)          // 返回 1404568027739
d = new Date();
d.getTime()        // 返回 1404568027739
```

###### 自动转换类型

当 JavaScript 尝试操作一个 "错误" 的数据类型时，会自动转换为 "正确" 的数据类型。


```javascript
5 + null    // 返回 5         because null is converted to 0
"5" + null  // 返回"5null"   because null is converted to "null"
"5" + 1     // 返回 "51"      because 1 is converted to "1" 
"5" - 1     // 返回 4         because "5" is converted to 5

document.getElementById("demo").innerHTML = myVar;

// if myVar = {name:"Fjohn"}  // toString 转换为 "[object Object]"
// if myVar = [1,2,3,4]       // toString 转换为 "1,2,3,4"
// if myVar = new Date()      // toString 转换为 "Fri Jul 18 2014 09:08:55 GMT+0200"

// if myVar = 123             // toString 转换为 "123"
// if myVar = true            // toString 转换为 "true"
// if myVar = false           // toString 转换为 "false"

var person = null; // 值为 null(空), 但类型为对象

var person; // 值为 undefined(空), 类型是undefined

```

#### 3.6.运算符

- [算数运算](#算数运算)
- [赋值运算](#赋值运算)
- [比较运算符](#比较运算符)
- [逻辑运算符](#逻辑运算符)
- [类型运算符](#类型运算符)
- [位运算符](#位运算符)
- [运算符优先级值](#运算符优先级值)

##### 算数运算

算数运算符用于对数字执行算数运算：

| 运算符 | 描述 |
| :----- | :--- |
| +      | 加法 |
| -      | 减法 |
| *      | 乘法 |
| /      | 除法 |
| %      | 系数 |
| ++     | 递加 |
| --     | 递减 |

##### 赋值运算

赋值运算符向 JavaScript 变量赋值。

| 运算符 | 例子   | 等同于    |
| :----- | :----- | :-------- |
| =      | x = y  | x = y     |
| +=     | x += y | x = x + y |
| -=     | x -= y | x = x - y |
| *=     | x *= y | x = x * y |
| /=     | x /= y | x = x / y |
| %=     | x %= y | x = x % y |


##### 比较预算符

| 运算符 | 描述           |
| :----- | :------------- |
| ==     | 等于           |
| ===    | 等值等型       |
| !=     | 不相等         |
| !==    | 不等值或不等型 |
| >      | 大于           |
| <      | 小于           |
| >=     | 大于或等于     |
| <=     | 小于或等于     |
| ?      | 三元运算符     |

##### 逻辑运算符

| 运算符 | 描述   |
| :----- | :----- |
| &&     | 逻辑与 |
| \|\|   | 逻辑或 |
| !      | 逻辑非 |

##### 类型运算符

| 运算符     | 描述                                  |
| :--------- | :------------------------------------ |
| typeof     | 返回变量的类型。                      |
| instanceof | 返回 true，如果对象是对象类型的实例。 |


##### 位运算符

| 运算符 | 描述         | 例子    | 等同于       | 结果 | 十进制 |
| :----- | :----------- | :------ | :----------- | :--- | :----- |
| &      | 与           | 5 & 1   | 0101 & 0001  | 0001 | 1      |
| \|     | 或           | 5 \| 1  | 0101 \| 0001 | 0101 | 5      |
| ~      | 非           | ~ 5     | ~0101        | 1010 | 10     |
| ^      | 异或         | 5 ^ 1   | 0101 ^ 0001  | 0100 | 4      |
| <<     | 零填充左位移 | 5 << 1  | 0101 << 1    | 1010 | 10     |
| >>     | 有符号右位移 | 5 >> 1  | 0101 >> 1    | 0010 | 2      |
| >>>    | 零填充右位移 | 5 >>> 1 | 0101 >>> 1   | 0010 | 2      |

##### 运算符优先级值

| 值   | 运算符     | 描述             | 实例             |
| :--- | :--------- | :--------------- | :--------------- |
| 20   | ( )        | 表达式分组       | (3 + 4)          |
|      |            |                  |                  |
| 19   | .          | 成员             | person.name      |
| 19   | []         | 成员             | person["name"]   |
| 19   | ()         | 函数调用         | myFunction()     |
| 19   | new        | 创建             | new Date()       |
|      |            |                  |                  |
| 17   | ++         | 后缀递增         | i++              |
| 17   | --         | 后缀递减         | i--              |
|      |            |                  |                  |
| 16   | ++         | 前缀递增         | ++i              |
| 16   | --         | 前缀递减         | --i              |
| 16   | !          | 逻辑否           | !(x==y)          |
| 16   | typeof     | 类型             | typeof x         |
|      |            |                  |                  |
| 15   | **         | 求幂 (ES7)       | 10 ** 2          |
|      |            |                  |                  |
| 14   | *          | 乘               | 10 * 5           |
| 14   | /          | 除               | 10 / 5           |
| 14   | %          | 模数除法         | 10 % 5           |
|      |            |                  |                  |
| 13   | +          | 加               | 10 + 5           |
| 13   | -          | 减               | 10 - 5           |
|      |            |                  |                  |
| 12   | <<         | 左位移           | x << 2           |
| 12   | >>         | 右位移           | x >> 2           |
| 12   | >>>        | 右位移（无符号） | x >>> 2          |
|      |            |                  |                  |
| 11   | <          | 小于             | x < y            |
| 11   | <=         | 小于或等于       | x <= y           |
| 11   | >          | 大于             | x > y            |
| 11   | >=         | 大于或等于       | x >= y           |
| 11   | in         | 对象中的属性     | "PI" in Math     |
| 11   | instanceof | 对象的实例       | instanceof Array |
|      |            |                  |                  |
| 10   | ==         | 相等             | x == y           |
| 10   | ===        | 严格相等         | x === y          |
| 10   | !=         | 不相等           | x != y           |
| 10   | !==        | 严格不相等       | x !== y          |
|      |            |                  |                  |
| 9    | &          | 按位与           | x & y            |
| 8    | ^          | 按位 XOR         | x ^ y            |
| 7    | \|         | 按位或           | x \| y           |
| 6    | &&         | 逻辑与           | x && y           |
| 5    | \|\|       | 逻辑否           | x \|\| y         |
| 4    | ? :        | 条件             | ? "Yes" : "No"   |
|      |            |                  |                  |
| 3    | =          | 赋值             | x = y            |
| 3    | +=         | 赋值             | x += y           |
| 3    | -=         | 赋值             | x -= y           |
| 3    | *=         | 赋值             | x *= y           |
| 3    | %=         | 赋值             | x %= y           |
| 3    | <<=        | 赋值             | x <<= y          |
| 3    | >>=        | 赋值             | x >>= y          |
| 3    | >>>=       | 赋值             | x >>>= y         |
| 3    | &=         | 赋值             | x &= y           |
| 3    | ^=         | 赋值             | x ^= y           |
| 3    | \|=        | 赋值             | x \|= y          |
|      |            |                  |                  |
| 2    | yield      | 暂停函数         | yield x          |
| 1    | ,          | 逗号             | 7 , 8            |

**提示：**括号中的表达式会在值在表达式的其余部分中被使用之前进行完全计算。

#### 3.7.保留关键字

保留关键字在意思上表达成为将来的关键字而保留的单词。

##### JavaScript 保留关键字

| abstract | arguments | boolean    | break     | byte         |
| -------- | --------- | ---------- | --------- | ------------ |
| case     | catch     | char       | class*    | const        |
| continue | debugger  | default    | delete    | do           |
| double   | else      | enum*      | eval      | export*      |
| extends* | false     | final      | finally   | float        |
| for      | function  | goto       | if        | implements   |
| import*  | in        | instanceof | int       | interface    |
| let      | long      | native     | new       | null         |
| package  | private   | protected  | public    | return       |
| short    | static    | super*     | switch    | synchronized |
| this     | throw     | throws     | transient | true         |
| try      | typeof    | var        | void      | volatile     |
| while    | with      | yield      |           |              |

\* 标记的关键字是 ECMAScript5 中新添加的。

##### JavaScript 对象、属性和方法

| Array     | Date     | eval     | function      | hasOwnProperty |
| --------- | -------- | -------- | ------------- | -------------- |
| Infinity  | isFinite | isNaN    | isPrototypeOf | length         |
| Math      | NaN      | name     | Number        | Object         |
| prototype | String   | toString | undefined     | valueOf        |

##### Java 保留关键字

JavaScript 经常与 Java 一起使用。您应该避免使用一些 Java 对象和属性作为 JavaScript 标识符：

| getClass | java | JavaArray |
| -------- | ---- | --------- |
|  javaClass        |   JavaObject   |       JavaPackage    |

##### Windows 保留关键字

| alert          | all                | anchor      | anchors            | area               |
| -------------- | ------------------ | ----------- | ------------------ | ------------------ |
| assign         | blur               | button      | checkbox           | clearInterval      |
| clearTimeout   | clientInformation  | close       | closed             | confirm            |
| constructor    | crypto             | decodeURI   | decodeURIComponent | defaultStatus      |
| document       | element            | elements    | embed              | embeds             |
| encodeURI      | encodeURIComponent | escape      | event              | fileUpload         |
| focus          | form               | forms       | frame              | innerHeight        |
| innerWidth     | layer              | layers      | link               | location           |
| mimeTypes      | navigate           | navigator   | frames             | frameRate          |
| hidden         | history            | image       | images             | offscreenBuffering |
| open           | opener             | option      | outerHeight        | outerWidth         |
| packages       | pageXOffset        | pageYOffset | parent             | parseFloat         |
| parseInt       | password           | pkcs11      | plugin             | prompt             |
| propertyIsEnum | radio              | reset       | screenX            | screenY            |
| scroll         | secure             | select      | self               | setInterval        |
| setTimeout     | status             | submit      | taint              | text               |
| textarea       | top                | unescape    | untaint            | window             |

##### HTML 事件句柄

| onblur    | onclick    | onerror     | onfocus     |
| --------- | ---------- | ----------- | ----------- |
| onkeydown | onkeypress | onkeyup     | onmouseover |
| onload    | onmouseup  | onmousedown | onsubmit    |

**注意：**在JavaScript中关键字不能用作变量名或者函数名，否则可能会得到错误消息，例如“"Identifier Expected"（应该有标识符、期望标识符）”。

### 四、流程

#### 4.1.条件

通常在写代码时，您总是需要为不同的决定来执行不同的动作。您可以在代码中使用条件语句来完成该任务。

- if 语句 - 只有当指定条件为 true 时，使用该语句来执行代码
- if...else 语句 - 当条件为 true 时执行代码，当条件为 false 时执行其他代码
- JavaScript三目运算 - 当条件为true 时执行代码，当条件为 false 时执行其他代码
- if...else if....else 语句- 使用该语句来选择多个代码块之一来执行
- switch 语句 - 使用该语句来选择多个代码块之一来执行


##### if

只有当指定条件为 true 时，该语句才会执行代码。

- 语法

```javascript
if (condition){
 当条件为 true 时执行的代码 
}

if (condition)  {
  当条件为 true 时执行的代码 
}
else{  
  当条件不为 true 时执行的代码  
}


if (condition1){
  当条件 1 为 true 时执行的代码 
}
else if (condition2){
 当条件 2 为 true 时执行的代码   
}  
else{
  当条件 1 和 条件 2 都不为 true 时执行的代码  
}
```

- 例子

```javascript
if (time<20){
  x="Good day";
}
else{
  x="Good evening";
}

5 > 3 ? alert("5大于3") : alert("5小于3");
```


##### switch

switch 语句用于在不同的条件执行不同的动作。搭配case和default使用（default可以认为是一个特殊的case，case对应一种或多种（default）情况，Switch语句没有case是没有办法体现其功能的）。

- 语法
  - 计算一次 switch 表达式
  - 把表达式的值与每个case的值进行对比
  - 如果存在匹配，则执行关联代码
```javascript
switch(n){
    case 1:
        执行代码块 1
        break;      
    case 2:      
        执行代码块 2      
        break;      
    default:
        n 与 case 1 和 case 2 不同时执行的代码
}
```


- 例子

```javascript
var x = "0";

switch (x) {

    case 0:

        text = "Off";

        break;

    case 1:

        text = "On";

        break;

    default:

        text = "No value found";

}
```

#### 4.2.循环

循环可以将代码块执行指定的次数。

- for - 循环代码块一定的次数
- for/in - 循环遍历对象的属性
- while - 当指定的条件为 true 时循环指定的代码块
- do/while - 同样当指定的条件为 true 时循环指定的代码块

##### for

- 语法
  - 语句 1 （代码块）开始前执行 starts.
  - 语句 2 定义运行循环（代码块）的条件
  - 语句 3 在循环（代码块）已被执行之后执行

```javascript
for (语句 1; 语句 2; 语句 3){        
  被执行的代码块        
}
```

- 例子
  - Statement 1 在循环开始之前设置变量 (var i=0)。
  - Statement 2 定义循环运行的条件（i 必须小于 5）。
  - Statement 3 在每次代码块已被执行后增加一个值 (i++)
  
```javascript
for (var i=0; i<5; i++){
  x=x + "The number is " + i + "<br>";
}

var i=0,len=cars.length;
for (; i<len; ){
    document.write(cars[i] + "<br>");
    i++;
}

```


##### while

while 循环会在指定条件为真时循环执行代码块。

- 语法

```javascript
while (条件){
 需要执行的代码
}

do{
需要执行的代码
}while (条件);

```

- 例子

```javascript
while (i<5){
  x=x + "The number is " + i + "<br>";
  i++;
}

do{
  x=x + "The number is " + i + "<br>";
  i++;
}while (i<5);

```

#### 4.3.跳转

- return 用于结束当前函数,并返回内容
- break 语句用于跳出循环。
- continue 用于跳过循环中的一个迭代。

##### Break

```javascript
for (i=0;i<10;i++){
  if (i==3){
    break;
  }
  x=x + "The number is " + i + "<br>";
}
```

##### Continue 

```javascript
for (i=0;i<=10;i++){
    if (i==3) continue;
    x=x + "The number is " + i + "<br>";
}
```

#### 4.4.异常处理

- try 语句测试代码块的错误。
- catch 语句处理错误。
- throw 语句创建自定义错误。

##### throw

throw 语句允许我们创建自定义错误。

- 语法

```javascript
throw exception 
```

- 例子

```javascript
var x=document.getElementById("demo").value;
if(x=="")    throw "empty";
```

##### try 和 catch

- 语法

```javascript
try{
   //在这里运行代码
}catch(err){
   //在这里处理错误
}

try{
   //在这里运行代码
}catch(err){
   //在这里处理错误
}finally{
  //无论错误和失败都会运行
}
```

- 实例

```javascript
var txt="";
function message(){
    try{
      adddlert("Welcome guest!");
    }catch(err){
      txt="本页有一个错误。\n\n";
      txt+="错误描述：" + err.message + "\n\n";
      txt+="点击确定继续。\n\n";
      alert(txt);
    }
}
```


### 五、函数

JavaScript 使用关键字 function 定义函数。函数可以通过声明定义，也可以是一个表达式。


#### 5.1.定义

- 函数声明

```javascript
function myFunction(a, b) {
    return a * b;
}
```

- 函数表达式

```javascript
var x = function (a, b) {return a * b};
```

- 构造函数

```javascript
var myFunction = new Function("a", "b", "return a * b");

var x = myFunction(4, 3);
```

- 函数提升

```javascript
// 提升（Hoisting）是 JavaScript 默认将当前作用域提升到前面去的的行为
myFunction(5);               
function myFunction(y) {        
    return y * y;        
}
```

#### 5.2.函数参数

JavaScript 函数参数与大多数其他语言的函数参数的区别在于：它不会关注有多少个参数被传递，不关注传递的参数的数据类型。

- 显式参数

```javascript
functionName(parameter1, parameter2, parameter3) {
    code to be executed
}
```

- 隐私参数 Arguments 包含了函数调用的参数数组

```javascript
x = sumAll(1, 123, 500, 115, 44, 88);

function sumAll() {
    var i, sum = 0;
    for (i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
}
```

- 默认参数

```javascript
function myFunction(x, y) {
    if (y === undefined) {
          y = 0;
    }
}
```


- 值传递

```javascript
var x = 1;
// 通过值传递参数
function myFunction(x) {
    x++; //修改参数x的值，将不会修改在函数外定义的变量 x
    console.log(x);
}
myFunction(x); // 2
console.log(x); // 1
```

- 对象传递参数
  
```javascript
var obj = {x:1};
// 通过对象传递参数
function myFunction(obj) {
    obj.x++; //修改参数对象obj.x的值，函数外定义的obj也将会被修改
    console.log(obj.x);
}
myFunction(obj); // 2
console.log(obj.x); // 2
```

#### 5.3.函数调用

JavaScript 函数有 4 种调用方式。
每种方式的不同在于 this 的初始化。
一般而言，在Javascript中，this指向函数执行时的当前对象。

- 作为一个函数调用

```javascript
function myFunction(a, b) {
    return a * b;
}
myFunction(10, 2);           // myFunction(10, 2) 返回 20

function myFunction() {
    return this;
}
myFunction();                // 返回 window 对象
```


- 函数作为方法调用

```javascript
var myObject = {
    firstName:"John",
    lastName: "Doe",
    fullName: function () {
        return this.firstName + " " + this.lastName;
    }
}
myObject.fullName();         // 返回 "John Doe"
```

- 使用构造函数调用函数

```javascript
// 构造函数:
function myFunction(arg1, arg2) {
    this.firstName = arg1;
    this.lastName  = arg2;
}

// This creates a new object
var x = new myFunction("John","Doe");
x.firstName;                             // 返回 "John"
```

- 作为函数方法调用函数

```javascript
function myFunction(a, b) {
    return a * b;
}
myFunction.call(myObject, 10, 2);      // 返回 20

myArray = [10,2];
myFunction.apply(myObject, myArray);   // 返回 20
```

#### 5.4.闭包

能访问函数内部的变量

```javascript
// 只有调用函数才能累计
var add = (function () {
    var counter = 0;
    return function () {return counter += 1;}
})();

add();
add();
add();

// 计数器为 3
```

More info: [JavaScript 参考手册](https://www.w3school.com.cn/jsref/index.asp)