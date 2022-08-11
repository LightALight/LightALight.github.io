---
title: JavaScript（二）JavaScript的基本知识(中)
date: 2016-11-15 19:23:32
tags: [web,javascript]
copyright: true
password:
toc: true
---

　　本文章主要介绍 JavaScript 的高级语法。

<!--more-->

## Quick Guide

### 一、HTML DOM

通过 HTML DOM，可访问 JavaScript HTML 文档的所有元素。

- JavaScript 能够改变页面中的所有 HTML 元素
- JavaScript 能够改变页面中的所有 HTML 属性
- JavaScript 能够改变页面中的所有 CSS 样式
- JavaScript 能够对页面中的所有事件做出反应

#### 1.1.查找 HTML 元素

- 通过 id 找到 HTML 元素

```JavaScript
var x=document.getElementById("intro");
```

- 通过标签名找到 HTML 元素

```JavaScript
var x=document.getElementById("main");
var y=x.getElementsByTagName("p");
```

- 通过类名找到 HTML 元素

```JavaScript
var x=document.getElementsByClassName("intro");
```

![](/image/JavaScript02/JavaScript02_001.png)


#### 1.2.改变 HTML 内容

- 改变 HTML 输出流

```html
<!DOCTYPE html>
<html>
<body>

<script>
document.write(Date());
</script>

</body>
</html>
```

- 改变 HTML 输出流

```html
<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML="New text!";
</script>

</body>
</html>
```

- 改变 HTML 输出流

```JavaScript
document.getElementById(id).attribute=new value
```

```html
<!DOCTYPE html>
<html>
<body>

<img id="image" src="smiley.gif">

<script>
document.getElementById("image").src="landscape.jpg";
</script>

</body>
</html>
```


#### 1.2.改变 改变 CSS

```JavaScript
document.getElementById(id).style.property=new style 
```

```html
<html>
<body>

<p id="p2">Hello World!</p>

<script>
document.getElementById("p2").style.color="blue";
</script>

<p>The paragraph above was changed by a script.</p>

</body>
</html>
```

#### 1.3.事件触发改变

在事件发生时执行 JavaScript，比如当用户在 HTML 元素上点击时。
- 当用户点击鼠标时
- 当网页已加载时
- 当图像已加载时
- 当鼠标移动到元素上时
- 当输入字段被改变时
- 当提交 HTML 表单时
- 当用户触发按键时

```JavaScript
onclick=JavaScript 
```

```html
<!DOCTYPE html>
<html>
<body>
<h1 onclick="this.innerHTML='Ooops!'">点击文本!</h1>
</body>
</html>

<button onclick="displayDate()">点我</button>
document.getElementById("myBtn").onclick=function(){displayDate()};
<body onload="checkCookies()">
<input type="text" id="fname" onchange="upperCase()">

```

- HTML 事件属性

```JavaScript
<button onclick="displayDate()">点我</button>
```

- 使用 HTML DOM 来分配事件

```JavaScript
document.getElementById("myBtn").onclick=function(){displayDate()};
```

- onload 和 onunload 事件:在用户进入或离开页面时被触发。

```JavaScript
<body onload="checkCookies()">
```

- onchange 事件

```JavaScript
<input type="text" id="fname" onchange="upperCase()">
```

#### 1.4.事件监听器

给页面的某些元素添加事件的监听器，当元素触发相应事件的时候监听器就会捕捉到这个事件并执行相应的代码。

- addEventListener() 
  - 用于向指定元素添加事件句柄。
  - 添加的事件句柄不会覆盖已存在的事件句柄。

```javascript
element.addEventListener(event, function, useCapture);
```

- 第一个参数是事件的类型 (如 "click" 或 "mousedown").
- 第二个参数是事件触发后调用的函数。
- 第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的。
  - 在冒泡中，内部元素的事件会先被触发，然后再触发外部元素，即： <p\> 元素的点击事件先触发，然后会触发 <div\> 元素的点击事件。
  - 在捕获中，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： <div\> 元素的点击事件先触发 ，然后再触发 <p\> 元素的点击事件。

```javascript
// 向原元素添加事件句柄
element.addEventListener("click", function(){ alert("Hello World!"); });

//向同一个元素中添加多个事件句柄
element.addEventListener("click", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);

//向 Window 对象添加事件句柄
window.addEventListener("resize", function(){
    document.getElementById("demo").innerHTML = sometext;
});

//传递参数
element.addEventListener("click", function(){ myFunction(p1, p2); });

```

- removeEventListener() 方法:移除由 addEventListener() 方法添加的事件句柄

**注意： IE 8 及更早 IE 版本，Opera 7.0及其更早版本不支持 addEventListener() 和 removeEventListener() 方法。**

```javascript
element.attachEvent(event, function);
element.detachEvent(event, function);
```

```javascript
element.removeEventListener("mousemove", myFunction);
```

#### 1.5.添加或删除 HTML 元素

- 创建新的 HTML 元素

```html
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("This is new.");
para.appendChild(node);

var element=document.getElementById("div1");
element.appendChild(para);
</script>
```

-删除已有的 HTML 元素

```html
<div id="div1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>
<script>
var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.removeChild(child);
</script>
```

### 二、表单

#### 2.1.获取表单元素

- select:下拉列表元素

```html
<div>
<label for="os">Operating System</label>
<select name="os" id="os">
    <option>Choose</option>
    <optgroup label="Windows">
        <option value="7 Home Basic">7 Home Basic</option>
        <option value="7 Home Premium">7 Home Premium</option>
        <option value="7 Professional">7 Professional</option>
        <option value="7 Ultimate">7 Ultimate</option>
        <option value="Vista">Vista</option>
        <option value="XP">XP</option>
    </optgroup>
<select>
</div>
```
```javascript
// 取到用户选择的值
var data = document.getElementById('selectMenu').value;

// 可以设置为多选
<select name="categories" id="categories" multiple>
var selected = [];
for (var i = 0, count = elem.options.length; i < count; i++) {
  if (elem.options[i].selected) {
    selected.push(elem.options[i].value);
  }
}
```
- checkbox:多选框控件，每个选择框只有选中和不选中两种状态。

```html
<input type="checkbox" name="toggle" id="toggle" value="toggle">

<!--checked属性返回一个布尔值，表示用户是否选中。-->
var which = document.getElementById('someCheckbox').checked;

<!--checked属性是可写的。-->
which.checked = true;

<!--value属性可以获取单选框的值。-->
if (which.checked) {
  var value = document.getElementById('someCheckbox').value;
}
```

- radio:单选框控件，同一组选择框同时只能选中一个，选中元素的checked属性为true。

```html
<input type="radio" name="gender" value="Male"> Male </input>
<input type="radio" name="gender" value="Female"> Female </input>
<script>
var radios = document.getElementsByName('gender');
var selected;
for (var i = 0; i < radios.length; i++) {
  if (radios[i].checked) {
    selected = radios[i].value;
    break;
  }
}
if (selected) {
  // 用户选中了某个选项
}
</script>
```

#### 2.2.表单的验证

所谓“表单验证”，指的是检查用户提供的数据是否符合要求。

- 必填（或必选）项目

```javascript
function validateForm() {        
    var x=document.forms["myForm"]["fname"].value;        
    if (x==null || x==""){        
        alert("First name must be filled out");        
        return false;        
    }        
}
```

- E-mail 验证

```javascript
function validateForm(){        
var x=document.forms["myForm"]["email"].value;        
var atpos=x.indexOf("@");        
var dotpos=x.lastIndexOf(".");        
if (atpos<1 || dotpos<atpos+2 || dotpos+2>=x.length){        
  alert("Not a valid e-mail address");        
  return false;        
  }       
}
```

- 数字验证

```html
<form name="myForm" action="demo_form.asp" onsubmit="return validateForm();" method="post">
<strong>请输入1到10之间的数字：</strong>
<input id="number">
<button type="button" onclick="myFunction()">提交</button>
</form>
```

### 三、正则表达式

正则表达式（英语：Regular Expression，在代码中常简写为regex、regexp或RE）使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式。

```javascript
var patt = /w3cschool/i
```
- /w3cschool/i  是一个正则表达式。
- w3cschool  是一个模式 (用于检索)。
- i 是一个修饰符 (搜索不区分大小写)。

#### 3.1.方法

##### 支持正则表达式的 String 对象的方法

- search() 方法:用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串，并返回子字符串的起始位置。

```javascript
var str = "Visit w3cschool"; 
var n = str.search(/w3cschool/i); //输出结果为：6
```

- replace() 方法: 用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子字符串。

```javascript
var str = "Visit Microsoft!";
var res = str.replace("Microsoft", "w3cschool");
```

- match:替换与正则表达式匹配的子串。

```javascript
var str="The rain in SPAIN stays mainly in the plain";
var n=str.match(/ain/g); //输出结果为：[ain,ain,ain]
```

- split:把字符串分割为字符串数组。	

```javascript
var str="How are you doing today?";
var n=str.split(" "); //输出结果为：[How,are,you,doing,today?]
```

##### 对象方法

- test():用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。

```javascript
var patt = /e/;
patt.test("The best things in life are free!"); // 输出结果:true
```

- exec():用于检索字符串中的正则表达式的匹配。

```javascript
/e/.exec("The best things in life are free!"); // 输出结果:e
```

- compile():既可以改变检索模式，也可以添加或删除第二个参数。

```javascript
var patt1=new RegExp("e");
document.write(patt1.test("The best things in life are free")); // true
patt1.compile("d");
document.write(patt1.test("The best things in life are free")); // false
```

#### 3.2.正则表达式修饰符

**修饰符** 可以在全局搜索中不区分大小写:

| 修饰符 | 描述                                                     |
| :----- | :------------------------------------------------------- |
| i      | 执行对大小写不敏感的匹配。                               |
| g      | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
| m      | 执行多行匹配。                                           |

#### 3.3.正则表达式模式

方括号用于查找某个范围内的字符：

| 表达式                                                       | 描述                               |
| :----------------------------------------------------------- | :--------------------------------- |
| [[abc\]](https://www.w3cschool.cn/jsref/jsref-regexp-charset.html) | 查找方括号之间的任何字符。         |
| [[^abc\]](https://www.w3cschool.cn/jsref/jsref-regexp-charset-not.html) | 查找任何不在方括号之间的字符。     |
| [0-9]                                                        | 查找任何从 0 至 9 的数字。         |
| [a-z]                                                        | 查找任何从小写 a 到小写 z 的字符。 |
| [A-Z]                                                        | 查找任何从大写 A 到大写 Z 的字符。 |
| [A-z]                                                        | 查找任何从大写 A 到小写 z 的字符。 |
| [adgk]                                                       | 查找给定集合内的任何字符。         |
| [^adgk]                                                      | 查找给定集合外的任何字符。         |
| (red\|blue\|green)                                           | 查找任何指定的选项。               |

元字符（Metacharacter）是拥有特殊含义的字符：

| 元字符                                                       | 描述                                        |
| :----------------------------------------------------------- | :------------------------------------------ |
| [.](https://www.w3cschool.cn/jsref/jsref-regexp-dot.html)    | 查找单个字符，除了换行和行结束符。          |
| [\w](https://www.w3cschool.cn/jsref/jsref-regexp-wordchar.html) | 查找单词字符。                              |
| [\W](https://www.w3cschool.cn/jsref/jsref-regexp-wordchar-non.html) | 查找非单词字符。                            |
| [\d](https://www.w3cschool.cn/jsref/jsref-regexp-digit.html) | 查找数字。                                  |
| [\D](https://www.w3cschool.cn/jsref/jsref-regexp-digit-non.html) | 查找非数字字符。                            |
| [\s](https://www.w3cschool.cn/jsref/jsref-regexp-whitespace.html) | 查找空白字符。                              |
| [\S](https://www.w3cschool.cn/jsref/jsref-regexp-whitespace-non.html) | 查找非空白字符。                            |
| [\b](https://www.w3cschool.cn/jsref/jsref-regexp-begin.html) | 匹配单词边界。                              |
| [\B](https://www.w3cschool.cn/jsref/jsref-regexp-begin-not.html) | 匹配非单词边界。                            |
| \0                                                           | 查找 NUL 字符。                             |
| [\n](https://www.w3cschool.cn/jsref/jsref-regexp-newline.html) | 查找换行符。                                |
| \f                                                           | 查找换页符。                                |
| \r                                                           | 查找回车符。                                |
| \t                                                           | 查找制表符。                                |
| \v                                                           | 查找垂直制表符。                            |
| [\xxx](https://www.w3cschool.cn/jsref/jsref-regexp-octal.html) | 查找以八进制数 xxx 规定的字符。             |
| [\xdd](https://www.w3cschool.cn/jsref/jsref-regexp-hex.html) | 查找以十六进制数 dd 规定的字符。            |
| [\uxxxx](https://www.w3cschool.cn/jsref/jsref-regexp-unicode-hex.html) | 查找以十六进制数 xxxx 规定的 Unicode 字符。 |

| 量词                                                         | 描述                                        |
| :----------------------------------------------------------- | :------------------------------------------ |
| [n+](https://www.w3cschool.cn/jsref/jsref-regexp-onemore.html) | 匹配任何包含至少一个 n 的字符串。           |
| [n*](https://www.w3cschool.cn/jsref/jsref-regexp-zeromore.html) | 匹配任何包含零个或多个 n 的字符串。         |
| [n?](https://www.w3cschool.cn/jsref/jsref-regexp-zeroone.html) | 匹配任何包含零个或一个 n 的字符串。         |
| [n{X}](https://www.w3cschool.cn/jsref/jsref-regexp-nx.html)  | 匹配包含 X 个 n 的序列的字符串。            |
| [n{X,Y}](https://www.w3cschool.cn/jsref/jsref-regexp-nxy.html) | 匹配包含 X 至 Y 个 n 的序列的字符串。       |
| [n{X,}](https://www.w3cschool.cn/jsref/jsref-regexp-nxcomma.html) | 匹配包含至少 X 个 n 的序列的字符串。        |
| [n$](https://www.w3cschool.cn/jsref/jsref-regexp-ndollar.html) | 匹配任何结尾为 n 的字符串。                 |
| [^n](https://www.w3cschool.cn/jsref/jsref-regexp-ncaret.html) | 匹配任何开头为 n 的字符串。                 |
| [?=n](https://www.w3cschool.cn/jsref/jsref-regexp-nfollow.html) | 匹配任何其后紧接指定字符串 n 的字符串。     |
| [?!n](https://www.w3cschool.cn/jsref/jsref-regexp-nfollow-not.html) | 匹配任何其后没有紧接指定字符串 n 的字符串。 |

### 四、JSON

JSON 英文全称 JavaScript Object Notation
JSON 是一种轻量级的数据交换格式。
JSON 是用于存储和传输数据的格式。
JSON 通常用于服务端向网页传递数据 。

#### 4.1.JSON 语法规则

- 数据为 键/值 对。
- 数据由逗号分隔。
- 大括号保存对象
- 方括号保存数组
                            
```json
"employees":[        
    {"firstName":"John", "lastName":"Doe"},        
    {"firstName":"Anna", "lastName":"Smith"},     
    {"firstName":"Peter", "lastName":"Jones"}        
]
```

#### 4.2.JSON 字符串转换为 JavaScript 对象

```javascript
var obj = JSON.parse(text);

```
### 五、对象
对象只是一种特殊的数据。对象拥有属性和方法。
JavaScript 提供多个内建对象，比如 String、Date、Array 等等。 对象只是带有属性和方法的特殊数据类型。

- 布尔型可以是一个对象。
- 数字型可以是一个对象。
- 字符串也可以是一个对象
- 日期是一个对象
- 数学和正则表达式也是对象
- 数组是一个对象
- 甚至函数也可以是对象

#### 5.1.对象的属性和方法

- 访问对象的属性

```javascript
objectName.propertyName 
```

```javascript
var message="Hello World!";
var x=message.length;
```

- 访问对象的方法

```javascript
objectName.methodName()

 for (variable in object)
 {
   //code to be executed
 }
```

```javascript
var message="Hello world!";
var x=message.toUpperCase();
```

#### 5.2.创建 JavaScript 对象

- 定义并创建对象的实例

```javascript
person=new Object();
person.firstname="John";
person.lastname="Doe";
person.age=50;
person.eyecolor="blue";
```

- 使用函数来定义对象，然后创建新的对象实例

```javascript
function person(firstname,lastname,age,eyecolor)
{
    this.firstname=firstname;
    this.lastname=lastname;
    this.age=age;
    this.eyecolor=eyecolor;
}
```

#### 5.3.给 JavaScript 增加属性和方法

```javascript
//把属性添加到 JavaScript 对象
person.firstname="John";
person.lastname="Doe";
person.age=30;
person.eyecolor="blue";

x=person.firstname;

// 把方法添加到 JavaScript 对象
 function person(firstname,lastname,age,eyecolor)
 {
     this.firstname=firstname;
     this.lastname=lastname;
     this.age=age;
     this.eyecolor=eyecolor;

     this.changeName=changeName;
     function changeName(name)
     {
           this.lastname=name;
     }
 }

```

#### 5.5.给 JavaScript 增加属性和方法


##### Number 对象

JavaScript 的 Number 对象是经过封装的能让你处理数字值的对象，由 Number() 构造器创建。

```javascript
var x = 123;
var y = new Number(123);
typeof(x) // returns Number
typeof(y) // returns Object
```
- Infinity:当数字运算结果超过了JavaScript所能表示的数字上限（溢出），结果为一个特殊的无穷大（infinity）值
- NaN 属性是代表非数字值的特殊值。该属性用于指示某个值不是数字。可以把 Number 对象设置为该值，来指示其不是数字值。

- 数字属性
  - MAX_VALUE
  - MIN_VALUE
  - NEGATIVE_INFINITY
  - POSITIVE_INFINITY
  - NaN
  - prototype
  - constructor
- 数字方法
  - toExponential()
  - toFixed()
  - toPrecision()
  - toString()
  - valueOf()

##### 字符串（String）对象

```javascript
var y = new String('hello');
```

- 属性:
  - length
  - prototype
  - constructor
- 方法:
  - charAt()
  - charCodeAt()
  - concat()
  - fromCharCode()
  - indexOf()
  - lastIndexOf()
  - match()
  - replace()
  - search()
  - slice()
  - split()
  - substr()
  - substring()
  - toLowerCase()
  - toUpperCase()
  - valueOf()

##### Date（日期）对象

- 创建日期

```javascript
new Date() // 当前日期和时间        
new Date(milliseconds) //返回从 1970 年 1 月 1 日至今的毫秒数        
new Date(dateString)        
new Date(year, month, day, hours, minutes, seconds, milliseconds)
```

- 设置日期

```javascript
var myDate=new Date();        
myDate.setFullYear(2010,0,14);
```

- 两个日期比较

```javascript
var x=new Date();        
x.setFullYear(2100,0,4);        
var today = new Date();                
if (x>today){        
  alert("Today is before 14th January 2100");        
}        
else{        
  alert("Today is after 14th January 2100");        
}
```

- Date 对象属性

| 属性                                                         | 描述                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [constructor](https://www.w3cschool.cn/jsref/jsref-constructor-date.html) | 返回对创建此对象的 Date 函数的引用。 |
| [prototype](https://www.w3cschool.cn/jsref/jsref-prototype-date.html) | 使您有能力向对象添加属性和方法。     |

- Date 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [getDate()](https://www.w3cschool.cn/jsref/jsref-getdate.html) | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。                  |
| [getDay()](https://www.w3cschool.cn/jsref/jsref-getday.html) | 从 Date 对象返回一周中的某一天 (0 ~ 6)。                     |
| [getFullYear()](https://www.w3cschool.cn/jsref/jsref-getfullyear.html) | 从 Date 对象以四位数字返回年份。                             |
| [getHours()](https://www.w3cschool.cn/jsref/jsref-gethours.html) | 返回 Date 对象的小时 (0 ~ 23)。                              |
| [getMilliseconds()](https://www.w3cschool.cn/jsref/jsref-getmilliseconds.html) | 返回 Date 对象的毫秒(0 ~ 999)。                              |
| [getMinutes()](https://www.w3cschool.cn/jsref/jsref-getminutes.html) | 返回 Date 对象的分钟 (0 ~ 59)。                              |
| [getMonth()](https://www.w3cschool.cn/jsref/jsref-getmonth.html) | 从 Date 对象返回月份 (0 ~ 11)。                              |
| [getSeconds()](https://www.w3cschool.cn/jsref/jsref-getseconds.html) | 返回 Date 对象的秒数 (0 ~ 59)。                              |
| [getTime()](https://www.w3cschool.cn/jsref/jsref-gettime.html) | 返回 1970 年 1 月 1 日至今的毫秒数。                         |
| [getTimezoneOffset()](https://www.w3cschool.cn/jsref/jsref-gettimezoneoffset.html) | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。              |
| [getUTCDate()](https://www.w3cschool.cn/jsref/jsref-getutcdate.html) | 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。              |
| [getUTCDay()](https://www.w3cschool.cn/jsref/jsref-getutcday.html) | 根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。               |
| [getUTCFullYear()](https://www.w3cschool.cn/jsref/jsref-getutcfullyear.html) | 根据世界时从 Date 对象返回四位数的年份。                     |
| [getUTCHours()](https://www.w3cschool.cn/jsref/jsref-getutchours.html) | 根据世界时返回 Date 对象的小时 (0 ~ 23)。                    |
| [getUTCMilliseconds()](https://www.w3cschool.cn/jsref/jsref-getutcmilliseconds.html) | 根据世界时返回 Date 对象的毫秒(0 ~ 999)。                    |
| [getUTCMinutes()](https://www.w3cschool.cn/jsref/jsref-getutcminutes.html) | 根据世界时返回 Date 对象的分钟 (0 ~ 59)。                    |
| [getUTCMonth()](https://www.w3cschool.cn/jsref/jsref-getutcmonth.html) | 根据世界时从 Date 对象返回月份 (0 ~ 11)。                    |
| [getUTCSeconds()](https://www.w3cschool.cn/jsref/jsref-getutcseconds.html) | 根据世界时返回 Date 对象的秒钟 (0 ~ 59)。                    |
| getYear()                                                    | 已废弃。 请使用 [getFullYear()](https://www.w3cschool.cn/jsref/jsref-getfullyear.html) 方法代替。 |
| [parse()](https://www.w3cschool.cn/jsref/jsref-parse.html)   | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数。           |
| [setDate()](https://www.w3cschool.cn/jsref/jsref-setdate.html) | 设置 Date 对象中月的某一天 (1 ~ 31)。                        |
| [setFullYear()](https://www.w3cschool.cn/jsref/jsref-setfullyear.html) | 设置 Date 对象中的年份（四位数字）。                         |
| [setHours()](https://www.w3cschool.cn/jsref/jsref-sethours.html) | 设置 Date 对象中的小时 (0 ~ 23)。                            |
| [setMilliseconds()](https://www.w3cschool.cn/jsref/jsref-setmilliseconds.html) | 设置 Date 对象中的毫秒 (0 ~ 999)。                           |
| [setMinutes()](https://www.w3cschool.cn/jsref/jsref-setminutes.html) | 设置 Date 对象中的分钟 (0 ~ 59)。                            |
| [setMonth()](https://www.w3cschool.cn/jsref/jsref-setmonth.html) | 设置 Date 对象中月份 (0 ~ 11)。                              |
| [setSeconds()](https://www.w3cschool.cn/jsref/jsref-setseconds.html) | 设置 Date 对象中的秒钟 (0 ~ 59)。                            |
| [setTime()](https://www.w3cschool.cn/jsref/jsref-settime.html) | setTime() 方法以毫秒设置 Date 对象。                         |
| [setUTCDate()](https://www.w3cschool.cn/jsref/jsref-setutcdate.html) | 根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。              |
| [setUTCFullYear()](https://www.w3cschool.cn/jsref/jsref-setutcfullyear.html) | 根据世界时设置 Date 对象中的年份（四位数字）。               |
| [setUTCHours()](https://www.w3cschool.cn/jsref/jsref-setutchours.html) | 根据世界时设置 Date 对象中的小时 (0 ~ 23)。                  |
| [setUTCMilliseconds()](https://www.w3cschool.cn/jsref/jsref-setutcmilliseconds.html) | 根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。                 |
| [setUTCMinutes()](https://www.w3cschool.cn/jsref/jsref-setutcminutes.html) | 根据世界时设置 Date 对象中的分钟 (0 ~ 59)。                  |
| [setUTCMonth()](https://www.w3cschool.cn/jsref/jsref-setutcmonth.html) | 根据世界时设置 Date 对象中的月份 (0 ~ 11)。                  |
| [setUTCSeconds()](https://www.w3cschool.cn/jsref/jsref-setutcseconds.html) | setUTCSeconds() 方法用于根据世界时 (UTC) 设置指定时间的秒字段。 |
| setYear()                                                    | 已废弃。请使用 [setFullYear()](https://www.w3cschool.cn/jsref/jsref-setfullyear.html) 方法代替。 |
| [toDateString()](https://www.w3cschool.cn/jsref/jsref-todatestring.html) | 把 Date 对象的日期部分转换为字符串。                         |
| toGMTString()                                                | 已废弃。请使用 [toUTCString()](https://www.w3cschool.cn/jsref/jsref-toutcstring.html) 方法代替。 |
| [toISOString()](https://www.w3cschool.cn/jsref/jsref-toisostring.html) | 使用 ISO 标准返回字符串的日期格式。                          |
| [toJSON()](https://www.w3cschool.cn/jsref/jsref-tojson.html) | 以 JSON 数据格式返回日期字符串。                             |
| [toLocaleDateString()](https://www.w3cschool.cn/jsref/jsref-tolocaledatestring.html) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。       |
| [toLocaleTimeString()](https://www.w3cschool.cn/jsref/jsref-tolocaletimestring.html) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。       |
| [toLocaleString()](https://www.w3cschool.cn/jsref/jsref-tolocalestring.html) | 据本地时间格式，把 Date 对象转换为字符串。                   |
| [toString()](https://www.w3cschool.cn/jsref/jsref-tostring-date.html) | 把 Date 对象转换为字符串。                                   |
| [toTimeString()](https://www.w3cschool.cn/jsref/jsref-totimestring.html) | 把 Date 对象的时间部分转换为字符串。                         |
| [toUTCString()](https://www.w3cschool.cn/jsref/jsref-toutcstring.html) | 根据世界时，把 Date 对象转换为字符串。                       |
| [UTC()](https://www.w3cschool.cn/jsref/jsref-utc.html)       | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。        |
| [valueOf()](https://www.w3cschool.cn/jsref/jsref-valueof-date.html) | 返回 Date 对象的原始值。                                     |

##### Array（数组）对象

```javascript
var cars = ["Saab", "Volvo", "BMW"];
```

- 属性

| 属性                                                         | 描述                             |
| :----------------------------------------------------------- | :------------------------------- |
| [constructor](https://www.w3cschool.cn/jsref/jsref-constructor-array.html) | 返回创建数组对象的原型函数。     |
| [length](https://www.w3cschool.cn/jsref/jsref-length-array.html) | 设置或返回数组元素的个数。       |
| [prototype](https://www.w3cschool.cn/project/jsref/jsref-prototype-array.html) | 允许你向数组对象添加属性或方法。 |

------

- 方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [concat()](https://www.w3cschool.cn/jsref/jsref-concat-array.html) | 连接两个或更多的数组，并返回结果。                           |
| [copyWithin().](https://www.w3cschool.cn/jsref/jsref-conwithin-array.html?RECACHE=1) | 从数组的指定位置拷贝元素到数组的另一个指定位置中。           |
| [entries().](https://www.w3cschool.cn/jsref/jsref-7tuv3mlq.html?RECACHE=1) | 返回数组的可迭代对象。                                       |
| [every()](https://www.w3cschool.cn/jsref/jsref-every.html)   | 检测数组元素的每个元素是否都符合条件。                       |
| [fill().](https://www.w3cschool.cn/jsref/jsref-zg4t3mlr.html?RECACHE=1) | 使用一个固定值来填充数组。                                   |
| [filter()](https://www.w3cschool.cn/jsref/jsref-filter.html) | 检测数组元素，并返回符合条件所有元素的数组。                 |
| [find().](https://www.w3cschool.cn/jsref/jsref-kqcp3mls.html?RECACHE=1) | 返回符合传入测试（函数）条件的数组元素。                     |
| [findIndex().](https://www.w3cschool.cn/jsref/jsref-kyd23mlt.html?RECACHE=1) | 返回符合传入测试（函数）条件的数组元素索引。                 |
| [forEach().](https://www.w3cschool.cn/jsref/foreach.html?RECACHE=1) | 数组每个元素都执行一次回调函数。                             |
| [from().](https://www.w3cschool.cn/jsref/jsref-zlf73mlu.html?RECACHE=1) | 通过给定的对象中创建一个数组。                               |
| [indexOf()](https://www.w3cschool.cn/jsref/jsref-indexof-array.html) | 搜索数组中的元素，并返回它所在的位置。                       |
| [join()](https://www.w3cschool.cn/jsref/jsref-join.html)     | 把数组的所有元素放入一个字符串。                             |
| [lastIndexOf()](https://www.w3cschool.cn/jsref/jsref-lastindexof-array.html) | 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。 |
| [map()](https://www.w3cschool.cn/jsref/jsref-map.html)       | 通过指定函数处理数组的每个元素，并返回处理后的数组。         |
| [pop()](https://www.w3cschool.cn/jsref/jsref-pop.html)       | 删除数组的最后一个元素并返回删除的元素。                     |
| [push()](https://www.w3cschool.cn/jsref/jsref-push.html)     | 向数组的末尾添加一个或更多元素，并返回新的长度。             |
| [reverse()](https://www.w3cschool.cn/jsref/jsref-reverse.html) | 反转数组的元素顺序。                                         |
| [shift()](https://www.w3cschool.cn/jsref/jsref-shift.html)   | 删除数组的第一个元素。                                       |
| [slice()](https://www.w3cschool.cn/jsref/jsref-slice-array.html) | 选取数组的的一部分，并返回一个新数组。                       |
| [some()](https://www.w3cschool.cn/jsref/jsref-some.html)     | 检测数组元素中是否有元素符合指定条件。                       |
| [sort()](https://www.w3cschool.cn/jsref/jsref-sort.html)     | 对数组的元素进行排序。                                       |
| [splice()](https://www.w3cschool.cn/jsref/jsref-splice.html) | 从数组中添加或删除元素。                                     |
| [toString()](https://www.w3cschool.cn/jsref/jsref-tostring-array.html) | 把数组转换为字符串，并返回结果。                             |
| [unshift()](https://www.w3cschool.cn/jsref/jsref-unshift.html) | 向数组的开头添加一个或更多元素，并返回新的长度。             |
| [valueOf()](https://www.w3cschool.cn/jsref/jsref-valueof-array.html) | 返回数组对象的原始值。                                       |

##### Boolean（布尔）对象

```javascript
var myBoolean=new Boolean();
```

- Boolean 对象属性

| 属性                                                         | 描述                                  |
| :----------------------------------------------------------- | :------------------------------------ |
| [constructor](https://www.w3cschool.cn/jsref/jsref-constructor-boolean.html) | 返回对创建此对象的 Boolean 函数的引用 |
| [prototype](https://www.w3cschool.cn/jsref/jsref-prototype-boolean.html) | 使您有能力向对象添加属性和方法。      |

- Boolean 对象方法

| 方法                                                         | 描述                               |
| :----------------------------------------------------------- | :--------------------------------- |
| [toString()](https://www.w3cschool.cn/jsref/jsref-tostring-boolean.html) | 把布尔值转换为字符串，并返回结果。 |
| [valueOf()](https://www.w3cschool.cn/jsref/jsref-valueof-boolean.html) | 返回 Boolean 对象的原始值。        |

##### Math（算数）对象

```javascript
var x=Math.PI;
var y=Math.sqrt(16);
```

- Math 对象属性

| 属性                                                         | 描述                                              |
| :----------------------------------------------------------- | :------------------------------------------------ |
| [E](https://www.w3cschool.cn/jsref/jsref-e.html)             | 返回算术常量 e，即自然对数的底数（约等于2.718）。 |
| [LN2](https://www.w3cschool.cn/jsref/jsref-ln2.html)         | 返回 2 的自然对数（约等于0.693）。                |
| [LN10](https://www.w3cschool.cn/jsref/jsref-ln10.html)       | 返回 10 的自然对数（约等于2.302）。               |
| [LOG2E](https://www.w3cschool.cn/jsref/jsref-log2e.html)     | 返回以 2 为底的 e 的对数（约等于 1.414）。        |
| [LOG10E](https://www.w3cschool.cn/jsref/jsref-log10e.html)   | 返回以 10 为底的 e 的对数（约等于0.434）。        |
| [PI](https://www.w3cschool.cn/jsref/jsref-pi.html)           | 返回圆周率（约等于3.14159）。                     |
| [SQRT1_2](https://www.w3cschool.cn/jsref/jsref-sqrt1-2.html) | 返回返回 2 的平方根的倒数（约等于 0.707）。       |
| [SQRT2](https://www.w3cschool.cn/jsref/jsref-sqrt2.html)     | 返回 2 的平方根（约等于 1.414）。                 |

- Math 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.w3cschool.cn/jsref/jsref-abs.html)      | 返回 x 的绝对值。                                            |
| [acos(x)](https://www.w3cschool.cn/jsref/jsref-acos.html)    | 返回 x 的反余弦值。                                          |
| [asin(x)](https://www.w3cschool.cn/jsref/jsref-asin.html)    | 返回 x 的反正弦值。                                          |
| [atan(x)](https://www.w3cschool.cn/jsref/jsref-atan.html)    | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。     |
| [atan2(y,x)](https://www.w3cschool.cn/jsref/jsref-atan2.html) | 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。 |
| [ceil(x)](https://www.w3cschool.cn/jsref/jsref-ceil.html)    | 对数进行上舍入。                                             |
| [cos(x)](https://www.w3cschool.cn/jsref/jsref-cos.html)      | 返回数的余弦。                                               |
| [exp(x)](https://www.w3cschool.cn/jsref/jsref-exp.html)      | 返回 Ex 的指数。                                             |
| [floor(x)](https://www.w3cschool.cn/jsref/jsref-floor.html)  | 对 x 进行下舍入。                                            |
| [log(x)](https://www.w3cschool.cn/jsref/jsref-log.html)      | 返回数的自然对数（底为e）。                                  |
| [max(x,y,z,...,n)](https://www.w3cschool.cn/jsref/jsref-max.html) | 返回 x,y,z,...,n 中的最高值。                                |
| [min(x,y,z,...,n)](https://www.w3cschool.cn/jsref/jsref-min.html) | 返回 x,y,z,...,n中的最低值。                                 |
| [pow(x,y)](https://www.w3cschool.cn/jsref/jsref-pow.html)    | 返回 x 的 y 次幂。                                           |
| [random()](https://www.w3cschool.cn/jsref/jsref-random.html) | 返回 0 ~ 1 之间的随机数。                                    |
| [round(x)](https://www.w3cschool.cn/jsref/jsref-round.html)  | 把数四舍五入为最接近的整数。                                 |
| [sin(x)](https://www.w3cschool.cn/jsref/jsref-sin.html)      | 返回数的正弦。                                               |
| [sqrt(x)](https://www.w3cschool.cn/jsref/jsref-sqrt.html)    | 返回数的平方根。                                             |
| [tan(x)](https://www.w3cschool.cn/jsref/jsref-tan.html)      | 返回角的正切。                                               |


##### Window对象 

Window 对象表示一个浏览器窗口或一个框架。在客户端 JavaScript 中，Window 对象是全局对象，所有的表达式都在当前的环境中计算。
- JavaScript document 对象
- JavaScript frames 对象
- JavaScript history 对象
- JavaScript location 对象
- JavaScript navigator 对象
- JavaScript screen 对象

![](/image/JavaScript02/JavaScript02_002.png)

**JavaScript 是面向对象的语言，但 JavaScript 不使用类。**

More info: [JavaScript教程](https://www.w3cschool.cn/javascript)