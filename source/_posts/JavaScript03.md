---
title: JavaScript（三）JavaScript的基本知识(下)
date: 2016-12-15 19:23:32
tags: [web,javascript]
copyright: true
password:
toc: true
---

　　本文章主要介绍 JavaScript 的相关知识。

<!--more-->

## Quick Guide

### 一、execCommand函数命令

execCommand方法是执行一个对当前文档，当前选择或者给出范围的命令。处理Html数据时常用

```
document.execCommand(sCommand[,交互方式, 动态参数])
```
- sCommand为指令参数（如下例中的”2D-Position”）
- 交互方式参数如果是true的话将显示对话框，如果为false的话，则不显示对话框
- 动态参数一般为一可用值或属性值（如下例中的”true”）。

```javascript
document.execCommand("2D-Position","false","true");
```
#### 1.1.指令参数及意义

```
2D-Position 允许通过拖曳移动绝对定位的对象。
AbsolutePosition 设定元素的 position 属性为“absolute”(绝对)。
BackColor 设置或获取当前选中区的背景颜色。
BlockDirLTR 目前尚未支持。
BlockDirRTL 目前尚未支持。
Bold 切换当前选中区的粗体显示与否。
BrowseMode 目前尚未支持。
Copy 将当前选中区复制到剪贴板。
CreateBookmark 创建一个书签锚或获取当前选中区或插入点的书签锚的名称。
CreateLink 在当前选中区上插入超级链接，或显示一个对话框允许用户指定要为当前选中区插入的超级链接的 URL。
Cut 将当前选中区复制到剪贴板并删除之。
Delete 删除当前选中区。
DirLTR 目前尚未支持。
DirRTL 目前尚未支持。
EditMode 目前尚未支持。
FontName 设置或获取当前选中区的字体。
FontSize 设置或获取当前选中区的字体大小。
ForeColor 设置或获取当前选中区的前景(文本)颜色。
FormatBlock 设置当前块格式化标签。
Indent 增加选中文本的缩进。
InlineDirLTR 目前尚未支持。
InlineDirRTL 目前尚未支持。
InsertButton 用按钮控件覆盖当前选中区。
InsertFieldset 用方框覆盖当前选中区。
InsertHorizontalRule 用水平线覆盖当前选中区。
InsertIFrame 用内嵌框架覆盖当前选中区。
InsertImage 用图像覆盖当前选中区。
InsertInputButton 用按钮控件覆盖当前选中区。
InsertInputCheckbox 用复选框控件覆盖当前选中区。
InsertInputFileUpload 用文件上载控件覆盖当前选中区。
InsertInputHidden 插入隐藏控件覆盖当前选中区。
InsertInputImage 用图像控件覆盖当前选中区。
InsertInputPassword 用密码控件覆盖当前选中区。
InsertInputRadio 用单选钮控件覆盖当前选中区。
InsertInputReset 用重置控件覆盖当前选中区。
InsertInputSubmit 用提交控件覆盖当前选中区。
InsertInputText 用文本控件覆盖当前选中区。
InsertMarquee 用空字幕覆盖当前选中区。
InsertOrderedList 切换当前选中区是编号列表还是常规格式化块。
InsertParagraph 用换行覆盖当前选中区。
InsertSelectDropdown 用下拉框控件覆盖当前选中区。
InsertSelectListbox 用列表框控件覆盖当前选中区。
InsertTextArea 用多行文本输入控件覆盖当前选中区。
InsertUnorderedList 切换当前选中区是项目符号列表还是常规格式化块。
Italic 切换当前选中区斜体显示与否。
JustifyCenter 将当前选中区在所在格式化块置中。
JustifyFull 目前尚未支持。
JustifyLeft 将当前选中区所在格式化块左对齐。
JustifyNone 目前尚未支持。
JustifyRight 将当前选中区所在格式化块右对齐。
LiveResize 迫使 MSHTML 编辑器在缩放或移动过程中持续更新元素外观，而不是只在移动或缩放完成后更新。
MultipleSelection 允许当用户按住 Shift 或 Ctrl 键时一次选中多于一个站点可选元素。
Open 目前尚未支持。
Outdent 减少选中区所在格式化块的缩进。
OverWrite 切换文本状态的插入和覆盖。
Paste 用剪贴板内容覆盖当前选中区。
PlayImage 目前尚未支持。
Print 打开打印对话框以便用户可以打印当前页。
Redo 目前尚未支持。
Refresh 刷新当前文档。
RemoveFormat 从当前选中区中删除格式化标签。
RemoveParaFormat 目前尚未支持。
SaveAs 将当前 Web 页面保存为文件。
SelectAll 选中整个文档。
SizeToControl 目前尚未支持。
SizeToControlHeight 目前尚未支持。
SizeToControlWidth 目前尚未支持。
Stop 目前尚未支持。
StopImage 目前尚未支持。
StrikeThrough 目前尚未支持。
Subscript 目前尚未支持。
Superscript 目前尚未支持。
UnBookmark 从当前选中区中删除全部书签。
Underline 切换当前选中区的下划线显示与否。
Undo 目前尚未支持。
Unlink 从当前选中区中删除全部超级链接。
Unselect 清除当前选中区的选中状态。
```

### 二、库

#### 2.1.jQuery

jQuery 是目前最受欢迎的 JavaScript 框架。
它使用 CSS 选择器来访问和操作网页上的 HTML 元素（DOM 对象）。
jQuery 同时提供 companion UI（用户界面）和插件。

```javascript
// JavaScript 
function myFunction(){
    var obj=document.getElementById("h01");
    obj.innerHTML="Hello jQuery";
}
onload=myFunction;

//jQuery 
function myFunction(){
    $("#h01").html("Hello jQuery");
}
$(document).ready(myFunction);
```
#### 2.2.Prototype

Prototype 提供的函数可使 HTML DOM 编程更容易。

```javascript
// JavaScript 
function myFunction(){
    var obj=document.getElementById("h01");
    obj.innerHTML="Hello Prototype";
}
onload=myFunction;

//Prototype 
function myFunction(){
    $("h01").insert("Hello Prototype!");
}
Event.observe(window,"load",myFunction);
```

#### 2.3.MooTools

虽然Mootools跟Prototype几乎拥有一样的语法，但是它提供了比Prototype多的功能，而且更强大，拥有实用而清晰的文档和示例帮助你轻松入门。



### 二、调试

#### 2.1.开启调试

- Chrome 浏览器
  - 打开浏览器。
  - 在菜单中选择工具。
  - 在工具中选择开发者工具。
  - 最后，选择 Console。
- Firefox 浏览器
  - 打开浏览器。
  - 访问页面:http://www.getfirebug.com。
  - 按照说明 :
    安装 Firebug。
- Internet Explorer 浏览器。
  - 打开浏览器。
  - 在菜单中选择工具。
  - 在工具中选择开发者工具。
  - 最后，选择 Console。
- Opera
  - 打开浏览器。
  - Opera 的内置调试工具为 Dragonfly，详细说明可访问页面:http://www.opera.com/dragonfly/。
- Safari
  - 打开浏览器。
  - 访问页面:http://extentions.apple.com。
  - 按说明操作：install Firebug Lite。


#### 2.2.调试方法

- console.log() 方法

```html
<!DOCTYPE html>
<html>
<body>

<h1>My First Web Page</h1>

<script>
a = 5;
b = 6;
c = a + b;
console.log(c);
</script>

</body>
</html>
```

- 设置断点
- debugger 

```javascript
var x = 15 * 5;
debugger;
document.getElementbyId("demo").innerHTML = x; //开启 debugger ，代码在第三行前停止执行。
```

### 三、代码规范

规范的代码可以更易于阅读与维护。

#### 3.1.变量名

- 推荐使用驼峰法来命名(camelCase):
- 变量名应该区分大小写，允许包含字母、数字、美元符号($)和下划线，但第一个字符不允许是数字，不允许包含空格和其他标点符号；
- 变量命名长度应该尽可能的短，并抓住要点，尽量在变量名中体现出值的类型；
- 变量名的命名应该是有意义的；
- 变量名不能为JavaScript中的关键词、保留字全名；
- 变量名命名方法常见的有匈牙利命名法、驼峰命名法和帕斯卡命名法。

```javascript
firstName = "John";
lastName = "Doe";

price = 19.90;
tax = 0.20;

fullPrice = price + (price * tax);
```

#### 3.2.空格与运算符

- 通常运算符 ( = + - * / ) 前后需要添加空格:

```javascript
var x = y + z;
var values = ["Volvo", "Saab", "Fiat"];
```

- 通常使用 4 个空格符号来缩进代码块：
```javascript
function toCelsius(fahrenheit) {
    return (5 / 9) * (fahrenheit - 32);
}
```

#### 3.3.语句规则

- 一条简单语句通常以分号作为结束符。

```javascript
var values = ["Volvo", "Saab", "Fiat"];

var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};
```

- 复杂语句的通用规则:
  - 将左花括号放在第一行的结尾。
  - 左花括号前添加一空格。
  - 将右花括号独立放在一行。
  - 不要忘记以分号结束一个复杂的声明。

```javascript
function toCelsius(fahrenheit) {
    return (5 / 9) * (fahrenheit - 32);
}
```

- 每行代码字符小于 80

#### 3.5.对象规则

对象定义的规则:
- 将左花括号与类名放在同一行。
- 冒号与属性值间有个空格。
- 字符串使用双引号，数字不需要。
- 最后一个属性-值对后面不要添加逗号。
- 将右花括号独立放在一行，并以分号作为结束符号。

```javascript
var person = {
    firstName: "John",
    lastName: "Doe",
    age: 50,
    eyeColor: "blue"
};
```

#### 3.6.命名规则

- 变量和函数为驼峰法（ camelCase）
- 全局变量为大写 (UPPERCASE )
- 常量 (如 PI) 为大写 (UPPERCASE )
- 使用简洁的格式载入 JavaScript 文件 ( type 属性不是必须的):

```html
<script src="myscript.js">
```
- HTML 与 JavaScript 尽量使用相同的命名规则。
- 使用小写文件名



### 四、性能

- 不要使用 with() 语句
  - 因为 with() 语句将会在作用域链的开始添加额外的变量。
  - 额外的变量意味着，当任何变量需要被访问的时候，JavaScript引擎都需要先扫描with()语句产生的变量，然后才是局部变量，最后是全局变量。  
  - 因此with()语句同时给局部变量和全局变量的性能带来负面影响，最终使我们优化JavaScript性能的计划破产。
- 避免全局查找
- 用"" + 1来将数字转换成字符串，虽然看起来比较丑一点，但事实上这个效率是最高的
```
("" +) > String() > .toString() > new String()
```
- 通过模板元素clone，替代createElement
- 避免低效率的脚本位置

```html
<!--低效率-->
<html>
<head>
    <title>Source Example</title>
    <script type="text/javascript" src="script1.js"></script>
    <script type="text/javascript" src="script2.js"></script>
    <script type="text/javascript" src="script3.js"></script>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
    <p>Hello world!</p>
</body>
</html>

<!--推荐-->
<head>
    <title>Source Example</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
    <p>Hello world!</p>
    <!-- Example of efficient script positioning -->
    <script type="text/javascript" src="script1.js"></script>
    <script type="text/javascript" src="script2.js"></script>
    <script type="text/javascript" src="script3.js"></script>
</body>
</html>
```
- 小心使用闭包
- 在循环时将控制条件和控制变量合并起来

```javascript
// 错误
for ( var x = 0; x < 10; x++ ) {
};

//正确
var x = 9;
do { } while( x-- );
```

- 使用 XMLHttpRequest(XHR)对象
  - 优点:下载不立即执行的 JavaScript 代码。由于代码返回在<script\>标签之外（换句话说不受<script\>标签约束），它下载后不会自动执行，这使得您可以推迟执行，直到一切都准备好了。另一个优点是，同样的代码在所有现代浏览器中都不会引发异常。
  - 缺点：JavaScript 文件必须与页面放置在同一个域内，不能从 CDN 下载（CDN 指”内容投递网络 Content Delivery Network）”，所以大型网页通常不采用 XHR 脚本注入技术。
- 最小化访问NodeList的次数可以极大的改进脚本的性能
- 避免与null进行比较
- 尊重对象的所有权
- 避免循环引用

```javascript
// 错误:init在执行的时候，当前上下文我们叫做context。这个时候，context引用了el，el引用了function，function引用了context。这时候形成了一个循环引用。
function init() {
    var el = document.getElementById('MyElement');
    el.onclick = function () {
    //……
    }
}
init();

//正确:置空dom对象
function init() {
    var el = document.getElementById('MyElement');
    el.onclick = function () {
    //……
    }
    try {
        return el;
    }
    finally {
        el = null;
    }
}
init();

//正确:构造新的context
function elClickHandler() {
//……
}
function init() {
    var el = document.getElementById('MyElement');
    el.onclick = elClickHandler;
}
init();
```

- 通过javascript创建的dom对象，必须append到页面中
- 字符串连接避免使用+=
- 使用直接量

```javascript
var aTest = new Array(); //替换为
var aTest = [];

var aTest = new Object; //替换为
var aTest = {};

var reg = new RegExp(); //替换为
var reg = /../;

//如果要创建具有一些特性的一般对象，也可以使用字面量，如下：
var oFruit = new O;
oFruit.color = "red";
oFruit.name = "apple";

//前面的代码可用对象字面量来改写成这样：
var oFruit = { color: "red", name: "apple" };
```

- 尽量少使用eval函数
- 不要给setTimeout或者setInterval传递字符串参数
- 缩短否定检测

```javascript
if(oTest != '#ff0000'){
    //do something
}
if(oTest != null){
//do something
}
if(oTest != false){
  //do something
}
//虽然这些都正确，但用逻辑非操作符来操作也有同样的效果：
if(!oTest){
//do something
}
```

- 释放javascript对象
- 尽量使用原生方法
- switch语句相对if较快
- 位运算较快
- 巧用||和&&布尔运算符

```javascript
function eventHandler(e) {
    if (!e) e = window.event;
}
//可以替换为：
function eventHandler(e) {
    e = e || window.event;
}
```

### 五、注意事项

- 每条语句末尾须加分号
- 使用+号时需谨慎
- 使用return语句需要注意不要用()括号来括住返回值，如果返回表达式，则表达式应与return关键字在同一行，以避免压缩时，压缩工具自动加分号而造成返回与开发人员不一致的结果
- 在比较是否相等的情况下，最好使用全等运行符，也就是使用===和!==操作符会相对于==和!=会好点。==和!=操作符会进行类型强制转换
- 不要使用生偏语法，写让人迷惑的代码，虽然计算机能够正确识别并运行，但是晦涩难懂的代码不方便以后维护
- 函数返回统一类型
- 总是检查数据类型
- 在HTML中使用双引号，在JavaScript中使用单引号，但为了兼容各个浏览器，也为了解析时不会出错，定义JSON对象时，最好使用双引号
- 用JSLint运行JavaScript验证器来确保没有语法错误或者是代码没有潜在的问题。
- 部署之前推荐使用压缩工具将JS文件压缩。
- 文件编码统一用UTF-8。
- JavaScript 程序应该尽量放在 .js 的文件中。

More info: [JavaScript教程](https://www.w3cschool.cn/javascrip)