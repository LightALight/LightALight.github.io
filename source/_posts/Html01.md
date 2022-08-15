---
title: HTML（一）HTML的基本概念
date: 2016-05-15 19:23:32
tags: [web,html]
copyright: true
password:
toc: true
---

HTML 是一种超文本标记语言 (Hyper Text Markup Language)。本文章主要介绍 HTML 的基本概念。

<!--more-->
## Quick Guide




### 一、HTML 标签
标记语言使用标记标签(markup tag)来描述网页 。HTML 标记标签通常被称为 HTML 标签 (HTML tag)。

- HTML 标签是由尖括号包围的关键词，比如 `<html>`

- HTML 标签通常是成对出现的，比如 `<b>` 和 `</b>`

- 标签对中的第一个标签是开始标签，第二个标签是结束标签

- 开始和结束标签也被称为开放标签和闭合标签

- HTML 标签对大小写不敏感 ，万维网联盟（W3C）在 HTML 4 中推荐使用小写，而在未来 (X)HTML 版本中强制使用小写。 

[HTML 标签参考手册](https://www.w3school.com.cn/tags/html_ref_byfunc.asp)


#### 1.HTML 的 基本标签


- 1.HTML 标题（Heading）：是通过 `<h1>` - `<h6>` 等标签进行定义的。

```html
<h1>This is a heading</h1>
<h2>This is a heading</h2>
<h3>This is a heading</h3>
```

- 2.HTML 段落:通过 `<p>` 标签进行定义的。

```html
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

- 3.HTML 链接:通过 `<a>` 标签进行定义的。在 href 属性中指定链接的地址。

```html
<a href="https://www.baidu.com/">This is a link</a>
```

- 4.HTML 图像:通过 `<img>` 标签进行定义的。图像的名称和尺寸是以属性的形式提供的。

```html
<img src="w3school.jpg" width="104" height="142" />
```

#### 2.HTML 标题标签

| 标签                                                 | 描述            |
| :--------------------------------------------------- | :------------ |
| `<html>`   | 定义 HTML 文档。 |
| `<body>`  | 定义文档的主体。 |
| `<h1> to <h6>`  | 定义 HTML 标题   |
| `<hr>`  | 定义水平线。     |
| `<!-->` | 定义注释。       |


```html
<html>
<body>
<!-- <h1> 定义最大的标题。<h6> 定义最小的标题 -->
<h1>This is a heading</h1>
<!-- 水平线
-->
<hr />
<!--[if IE 8]>
    .... 只有 Internet Explorer 显示注释....
<![endif]-->
<h2>This is a heading</h2>
<h3>This is a heading</h3>
</body>
</html>
```

#### 3.HTML 段落标签

| 标签                                            | 描述                   |
| :------------------------------------- | :----------------- |
| `<p>`  | 定义段落。             |
| `<br />` | 插入单个折行（换行）。 |

```html
<html>
<body>
<h1>我的第一个标题</h1>
<p>我的第一个段落。</p>
<br />
<p>我的第一个段落。</p>
</body>
</html>
```

#### 4.HTML 格式化标签

- 文本格式化

| 标签                                | 描述     |
| :------------------------------- | :------------------------ |
| `<b>`      | 定义粗体文本。                        |
| `<big>`    | 定义大号字。                          |
| `<em>`| 定义着重文字。                        |
| `<i>`    | 定义斜体字。                          |
| `<small>`   | 定义小号字。                          |
| `<strong>`| 定义加重语气。                        |
| `<sub>`             | 定义下标字。                          |
| `<sup>`            | 定义上标字。                          |
| `<ins>`            | 定义插入字。                          |
| `<del>`          | 定义删除字。                          |

```html
<html>
<body>

<b>This text is bold</b>

<br />

<strong>This text is strong</strong>

<br />

<big>This text is big</big>

<br />

<em>This text is emphasized</em>

<br />

<i>This text is italic</i>

<br />

<small>This text is small</small>

<br />

This text contains
<sub>subscript</sub>

<br />

This text contains
<sup>superscript</sup>

</body>
</html>
```

- 计算机输出

|标签                   | 描述                            |
| :------------------------------ | :------------------------------ |
| `<code>` | 定义计算机代码。                |
| `<kbd>` | 定义键盘码。                    |
|`<samp>` | 定义计算机代码样本。            |
| `<tt>`      | 定义打字机代码。                |
| `<var>` | 定义变量。                      |
| `<pre>`           | 定义预格式文本。                |

```html
<html>
<body>

<code>
<pre>
var person = {
    firstName:"Bill",
    lastName:"Gates",
    age:50,
    eyeColor:"blue"
}
</pre>
</code>
<br />
<kbd>Keyboard input</kbd>
<br />
<tt>Teletype text</tt>
<br />
<samp>Sample text</samp>
<br />
<var>Computer variable</var>
<br />

<p>
<b>注释：</b>这些标签常用于显示计算机/编程代码。
</p>

</body>
</html>
```

- 引用、引用和术语定义

| 标签  | 描述               |
| :--------------------------------------- | :----------------- |
| `<abbr>`       | 定义缩写。         |
| `<acronym>`       | 定义首字母缩写。   |
| `<address>`      | 定义地址。         |
| `<bdo>`            | 定义文字方向。     |
| `<blockquote>`    | 定义长的引用。     |
| `<q>`           | 定义短的引用语。   |
| `<cite>` | 定义引用、引证。   |
| `<dfn>` | 定义一个定义项目。 |

```html
<html>
<body>

<p>WWF 的目标是：<q>构建人与自然和谐共存的世界。</q></p>
<br />

<p>以下内容引用自 WWF 的网站：</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>
<br />

<p><abbr title="World Health Organization">WHO</abbr> 成立于 1948 年。</p>
<br />

<p><dfn><abbr title="World Health Organization">WHO</abbr></dfn> 成立于 1948 年。</p>
<br />
    
<address>
Written by Donald Duck.<br> 
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
<br />

<p><cite>The Scream</cite> by Edward Munch. Painted in 1893.</p>
<br />

<bdo dir="rtl">This text will be written from right to left</bdo>

</body>
</html>
```

#### 5.HTML 链接标签

| 标签                                           | 描述     |
| :--------------------------------------------- | :------- |
| `href` | 定义锚。 |

HTML 使用超级链接与网络上的另一个文档相连，点击链接可以从一张页面跳转到另一张页面。
有两种使用 <a> 标签的方式：

- 通过使用 href 属性 - 创建指向另一个文档的链接

```html
<a href="https://www.baidu.com/">百度一下</a>
```

- 通过使用 name 属性 - 创建文档内的书签

```html
<a name="tips">基本的注意事项</a>
```

#### 6.HTML 图像标签

| 标签                         | 描述                         |
| :----------------------------- | :--------------------------- |
| `<img>`  | 定义图像。                   |
| `<map>`  | 定义图像地图。               |
| `<area>` | 定义图像地图中的可点击区域。 |

通过使用 HTML，可以在文档中显示图像。

```html
<img src="planets.jpg" border="0" usemap="#planetmap" alt="Planets" />

<map name="planetmap" id="planetmap">
  <area shape="circle" coords="180,139,14" href ="venus.html" alt="Venus" />
  <area shape="circle" coords="129,161,10" href ="mercur.html" alt="Mercury" />
  <area shape="rect" coords="0,0,110,260" href ="sun.html" alt="Sun" />
</map>
```

##### HTML 文件路径

| 路径                   | 描述                                         |
| :------------------- | :--------------------------- |
| `<img src="picture.jpg">`        | picture.jpg 位于与当前网页相同的文件夹       |
| `<img src="images/picture.jpg">`  | picture.jpg 位于当前文件夹的 images 文件夹中 |
| `<img src="/images/picture.jpg">` | picture.jpg 当前站点根目录的 images 文件夹中 |
| `<img src="../picture.jpg">`      | picture.jpg 位于当前文件夹的上一级文件夹中   |

#### 7.HTML表格 标签

| 表格                         | 描述                   |
| :------------------------------- | :--------------------- |
| `<table>` | 定义表格               |
| `<caption>` | 定义表格标题。         |
| `<th>`     | 定义表格的表头。       |
|   `<tr>`                             | 定义表格的行。         |
|  `<td>`    | 定义表格单元。         |
|   `<thead>`                        | 定义表格的页眉。       |
|  `<tbody>`                         | 定义表格的主体。       |
|  `<tfoot>`                                    | 定义表格的页脚。       |
|   `<col>`                                 | 定义用于表格列的属性。 |
|  `<colgroup>`                             | 定义表格列的组。       |


```html
<html>
<body>

<table border="1">
<caption>横跨两列的单元格</caption>
<tr>
  <th>姓名</th>
  <th colspan="2">电话</th>
</tr>
<tr>
  <td>Bill Gates</td>
  <td>555 77 854</td>
  <td>555 77 855</td>
</tr>
</table>

<br/>
<table border="1">
<caption>横跨两行的单元格</caption>
<tr>
  <th>姓名</th>
  <td>Bill Gates</td>
</tr>
<tr>
  <th rowspan="2">电话</th>
  <td>555 77 854</td>
</tr>
<tr>
  <td>555 77 855</td>
</tr>
</table>

</body>
</html>

```

#### 8.HTML 列表标签


| 标签                                            | 描述             |
| :---------------------------------------------- | :--------------- |
| `<ol>`| 定义有序列表。   |
| `<ul>` | 定义无序列表。   |
| `<li>` | 定义列表项。     |
| `<dl>` | 定义定义列表。   |
| `<dt>` | 定义定义项目。   |
| `<dd>` | 定义定义的描述。 |

- 无序列表：始于 `<ul>` 标签，每个列表项始于 `<li>`。

```html
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>
```

- 有序列表:始于 `<ol>` 标签,每个列表项始于 `<li>` 标签。

```html
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
```


### 二、HTML 元素

HTML 元素是由 HTML 标签 和 纯文本 构成。
HTML 元素：是从开始标签（start tag 或者叫做 开放标签（opening tag） ）到结束标签（end tag 或者叫做 闭合标签（closing tag） ）的所有代码。

| 开始标签                | 元素内容            | 结束标签 |
| :---------------------- | :------------------ | :------- |
| `<p>`                     | This is a paragraph | `</p>`     |
| `<a href="default.htm" >` | This is a link      | `</a>`     |
| `<br />`                  |                     |          |



### 三、HTML 文档
HTML 文档是由嵌套的 HTML 元素构成，用来描述网页。Web 浏览器的作用是读取 HTML 文档，并以网页的形式显示出它们。

```html
<!DOCTYPE html>
<html>
<head>
<title>Title of the document</title>
</head>

<body>
The content of the document......
</body>

</html>
```
#### HTML 文档类型
<!DOCTYPE> 声明帮助浏览器正确地显示网页。

- HTML5
```html
<!DOCTYPE html>
```

- HTML 4.01
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/html4/loose.dtd">
```

- XHTML 1.0
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

#### HTML 头部元素

| 标签                       | 描述                                     |
| :---------------------- | :--------------------------------------- |
| `<head>`  | 定义关于文档的信息。                     |
| `title` | 定义文档标题。                           |
| `base`  | 定义页面上所有链接的默认地址或默认目标。 |
| `link` | 定义文档与外部资源之间的关系。           |
| `<meta>`  | 定义关于 HTML 文档的元数据。             |
| `<script>` | 定义客户端脚本。                         |
| `<style>` | 定义文档的样式信息。                     |




### 四、HTML 编写网页

#### 选择合适的编辑器

- 文本编辑器
	- Notepad (PC) 
	- TextEdit (Mac)
- 专业的 HTML 编辑器
	- Adobe Dreamweaver
	- Microsoft Expression Web
	- CoffeeCup HTML Editor

#### 遍写步骤

- 1.启动编辑器
- 2.在编辑器中键入 HTML 代码，如下：
```html
<!DOCTYPE HTML> 
<html>
<body>
<h1>我的第一个标题</h1>
<p>我的第一个段落。</p>
</body>
</html>
```

- 3.保存为HTML文件(后缀为 .htm 或者 .html )
- 4.在浏览器中运行这个 HTML 文件



### 五、HTML 属性

HTML 标签拥有属性。属性提供了有关 HTML 元素的更多信息。
属性总是以名称/值对的形式出现，比如：name="value"。
属性总是在 HTML 元素的开始标签中规定。

例如：
```html
<a href="http://www.baidu.com">This is a link</a>
```

 [HTML 标准属性参考手册](https://www.w3school.com.cn/tags/html_ref_standardattributes.asp) 


### 六、HTML 样式 


| 标签                      | 描述                           |
| :------------------------ | :----------------------------- |
| `<style>` | 定义样式定义。                 |
| `<link>` | 定义资源引用。                 |

定义HTML 元素的样式:
- style 属性(内联样式)

```html
<html>
<!--background-color 属性为元素定义了背景颜色 -->
<body style="background-color:yellow">
<!-- text-align 属性规定了元素中文本的水平对齐方式 -->
<h1 style="text-align:center">This is a heading</h1>
<!--font-family、color 以及 font-size 属性分别定义元素中文本的字体系列、颜色和字体尺寸-->
<p style="font-family:arial;color:red;font-size:20px;">A paragraph.</p>
</body>
</html>
```

- 独立的样式表中（CSS 文件）
	- 外部样式表
	```html
	<head>
	<link rel="stylesheet" type="text/css" href="mystyle.css">
	</head>
	```
	
	- 内部样式表
	```html
	<head>
	
	<style type="text/css">
	body {background-color: red}
	p {margin-left: 20px}
	</style>
	</head>
	```


#### HTML 类
对 HTML 块级元素 进行分类（设置类），使我们能够为元素的类定义 CSS 样式。


```html
<!DOCTYPE html>
<html>
<head>
<style>
.cities {
    background-color:black;
    color:white;
    margin:20px;
    padding:20px;
} 
</style>
</head>

<body>

<div class="cities">
<h2>London</h2>
<p>London is the capital city of England. 
It is the most populous city in the United Kingdom, 
with a metropolitan area of over 13 million inhabitants.</p>
</div>

<div class="cities">
<h2>Paris</h2>
<p>Paris is the capital and most populous city of France.</p>
</div>

<div class="cities">
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.</p>
</div>

</body>
</html>
```

- 分类行内元素：例如设置 `<span>` 元素的类，能够为相同的 `<span>` 元素设置相同的样式。

```html
<!DOCTYPE html>
<html>
<head>
<style>
  span.red {color:red;}
</style>
</head>
<body>

<h1>My <span class="red">Important</span> Heading</h1>

</body>
</html>
```
#### HTML 颜色

可以通过颜色值和颜色名设置

- 颜色值：由红色、绿色和蓝色的值组成（RGB）

| Color  | Color HEX | Color RGB        |
| :----- | :-------- | :--------------- |
| 黑色   | #000000   | rgb(0,0,0)       |
| 红色   | #FF0000   | rgb(255,0,0)     |
| 绿色   | #00FF00   | rgb(0,255,0)     |
| 蓝色   | #0000FF   | rgb(0,0,255)     |
| 黄色   | #FFFF00   | rgb(255,255,0)   |
| 浅蓝色 | #00FFFF   | rgb(0,255,255)   |
| 紫色   | #FF00FF   | rgb(255,0,255)   |
| 灰色   | #C0C0C0   | rgb(192,192,192) |
| 白色   | #FFFFFF   | rgb(255,255,255) |


- 颜色名：仅仅有 16 种颜色名被 W3C 的 HTML4.0 标准所支持。它们是：aqua, black, blue, fuchsia, gray, green, lime, maroon, navy, olive, purple, red, silver, teal, white, yellow。如果需要使用其它的颜色，需要使用十六进制的颜色值。

| Color    | Color HEX | Color Name   |
| :------- | :-------- | :----------- |
| 爱丽丝蓝 | #F0F8FF   | AliceBlue    |
| 古董白   | #FAEBD7   | AntiqueWhite |
| 蓝晶     | #7FFFD4   | Aquamarine   |
| 黑色     | #000000   | Black        |
| 蓝色     | #0000FF   | Blue         |
| 紫罗兰   | #8A2BE2   | BlueViolet   |
| 棕色     | #A52A2A   | Brown        |

[颜色列表](https://www.w3school.com.cn/html/html_colornames.asp)


### 七、HTML 布局

#### HTML 块

| 标签                                              | 描述|
| :------------------------------ | :------------------------------- |
| `<div>` | 定义文档中的分区或节（division/section）。 |
| `<span>` | 定义 span，用来组合文档中的行内元素。      |

- `<div>` 元素:块级元素，它是可用于组合其他 HTML 元素的容器。用途是文档布局,如果与 CSS 一同使用，可用于对大的内容块设置样式属性。
- `<span>` 元素:内联元素，可用作文本的容器。与 CSS 一同使用时，可用于为部分文本设置样式属性。


#### HTML5 语义元素

| 语义元素 | 说明 |
| ------- | ------------------------------ |
| header  | 定义文档或节的页眉             |
| nav     | 定义导航链接的容器             |
| section | 定义文档中的节                 |
| article | 定义独立的自包含文章           |
| aside   | 定义内容之外的内容（比如侧栏） |
| footer  | 定义文档或节的页脚             |
| details | 定义额外的细节                 |
| summary | 定义 details 元素的标题        |

```html
<!DOCTYPE html>
<html>

<head>
<style>
#header {
    background-color:black;
    color:white;
    text-align:center;
    padding:5px;
}
#nav {
    line-height:30px;
    background-color:#eeeeee;
    height:300px;
    width:100px;
    float:left;
    padding:5px;	      
}
#section {
    width:350px;
    float:left;
    padding:10px;	 	 
}
#footer {
    background-color:black;
    color:white;
    clear:both;
    text-align:center;
   padding:5px;	 	 
}
</style>
</head>

<body>

<div id="header">
<h1>The Title</h1>
</div>

<div id="nav">
File<br>
View<br>
Help<br>
</div>

<div id="section">
<h2>Hello World</h2>
</div>

<div id="footer">
GoodBye
</div>

</body>
</html>
```


#### 使用表格的 HTML 布局

```html
<!DOCTYPE html>
<html>
<head>
<style>
table.lamp {
    width:100%;
    border:1px solid #d4d4d4;
}
table.lamp th, td { 
    padding:10px;
}
table.lamp th {
    width:40px;
}

</style>
</head>

<body>
 
<table class="lamp">
<tr>
  <th>
    <img src="/images/lamp.jpg" alt="Note" style="height:32px;width:32px">
  </th>
  <td>
    The table element was not designed to be a layout tool.
  </td>
</tr>
</table>

</body>
</html>
```

### 八、HTML 响应式 Web 设计

- RWD 指的是响应式 Web 设计（Responsive Web Design）
- RWD 能够以可变尺寸传递网页
- RWD 对于平板和移动设备是必需的

#### 自定义

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<style>
.city {
float: left;
margin: 5px;
padding: 15px;
width: 300px;
height: 300px;
border: 1px solid black;
} 
</style>
</head>

<body>

<h1>W3School Demo</h1>
<h2>Resize this responsive page!</h2>
<br>

<div class="city">
<h2>London</h2>
<p>London is the capital city of England.</p>
<p>It is the most populous city in the United Kingdom,
with a metropolitan area of over 13 million inhabitants.</p>
</div>

<div class="city">
<h2>Paris</h2>
<p>Paris is the capital and most populous city of France.</p>
</div>

<div class="city">
<h2>Tokyo</h2>
<p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
and the most populous metropolitan area in the world.</p>
</div>

</body>
</html>
```

#### 使用 Bootstrap

Bootstrap 是最流行的开发响应式 web 的 HTML, CSS, 和 JS 框架。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" 
  href="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
</head>

<body>

<div class="container">
<div class="jumbotron">
  <h1>W3School Demo</h1> 
  <p>Resize this responsive page!</p> 
</div>
</div>

<div class="container">
<div class="row">
  <div class="col-md-4">
    <h2>London</h2>
    <p>London is the capital city of England.</p>
    <p>It is the most populous city in the United Kingdom,
    with a metropolitan area of over 13 million inhabitants.</p>
  </div>
  <div class="col-md-4">
    <h2>Paris</h2>
    <p>Paris is the capital and most populous city of France.</p>
  </div>
  <div class="col-md-4">
    <h2>Tokyo</h2>
    <p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
    and the most populous metropolitan area in the world.</p>
  </div>
</div>
</div>

</body>
</html>
```


### 九、HTML 框架

#### HTML Frameset
通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。

使用框架的坏处：
- 开发人员必须同时跟踪更多的HTML文档
- 很难打印整张页面

框架结构标签（`<frameset>`）
框架结构标签（`<frameset>`）定义如何将窗口分割为框架,每个 frameset 定义了一系列行或列,rows/columns 的值规定了每行或每列占据屏幕的面积.



- 竖直框架
```html
<html>
<frameset cols="25%,50%,25%">
  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">

<noframes>
<body>您的浏览器无法处理框架！</body>
</noframes>

</frameset>
</html>
```

- 水平框架
```html
<html>
<frameset rows="25%,50%,25%">

  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">

</frameset>
</html>
```
#### HTML Iframe

iframe 用于在网页内显示网页。

- 设置高度和宽度
```
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
```

- 删除边框
```
<iframe src="demo_iframe.htm" frameborder="0"></iframe>
```

- 可用作链接的目标
```
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="http://www.baidu.com" target="iframe_a">baidu</a></p>
```



### 十、HTML 脚本

`<script>` 标签用于定义客户端脚本，比如 JavaScript。script 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。必需的 type 属性规定脚本的 MIME 类型。

JavaScript 最常用于图片操作、表单验证以及内容动态更新。

| 标签                            | 描述             |
| :------------------------ | :----------------------- |
| `<script>`   | 定义客户端脚本。         |
| `<noscript>` | 为不支持客户端脚本的浏览器定义替代内容。 |

下面的脚本会向浏览器输出“Hello World!”：

```html
<html>
<body>
<script type="text/javascript">
document.write("Hello World!")
</script>
<noscript>Your browser does not support JavaScript!</noscript>
</body>
</html>
```


### 十一、HTML 转换

#### HTML 字符实体

HTML 中的预留字符要在页面展示，必须被替换为字符实体。

**注释：**实体名称对大小写敏感！

| 显示结果 | 描述              | 实体名称          | 实体编号 |
| :------- | :---------------- | :---------------- | :------- |
|          | 空格              | &nbsp;            | &#160;   |
| <        | 小于号            | &lt;              | &#60;    |
| >        | 大于号            | &gt;              | &#62;    |
| &        | 和号              | &amp;             | &#38;    |
| "        | 引号              | &quot;            | &#34;    |
| '        | 撇号              | &apos; (IE不支持) | &#39;    |
| ￠       | 分（cent）        | &cent;            | &#162;   |
| £        | 镑（pound）       | &pound;           | &#163;   |
| ¥        | 元（yen）         | &yen;             | &#165;   |
| €        | 欧元（euro）      | &euro;            | &#8364;  |
| §        | 小节              | &sect;            | &#167;   |
| ©        | 版权（copyright） | &copy;            | &#169;   |
| ®        | 注册商标          | &reg;             | &#174;   |
| ™        | 商标              | &trade;           | &#8482;  |
| ×        | 乘号              | &times;           | &#215;   |
| ÷        | 除号              | &divide;          | &#247;   |

 [HTML 实体符号参考手册](https://www.w3school.com.cn/tags/html_ref_entities.html)

#### HTML URL

URL（Uniform Resource Locator,统一资源定位器） 也被称为网址。

```
scheme://host.domain:port/path/filename
```
解释：

- scheme - 定义因特网服务的类型。最常见的类型是 http
- host - 定义域主机（http 的默认主机是 www）
- domain - 定义因特网域名，比如 w3school.com.cn
- :port - 定义主机上的端口号（http 的默认端口号是 80）
- path - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
- filename - 定义文档/资源的名称

以下是其中一些最流行的 scheme：

| Scheme | 访问               | 用于...                             |
| :----- | :----------------- | :---------------------------------- |
| http   | 超文本传输协议     | 以 http:// 开头的普通网页。不加密。 |
| https  | 安全超文本传输协议 | 安全网页。加密所有信息交换。        |
| ftp    | 文件传输协议       | 用于将文件下载或上传至网站。        |
| file   |                    | 您计算机上的文件。                  |


- URL 编码：URL 只能使用 ASCII 字符集来通过因特网进行发送。ASCII 集合之外的字符，使用 "%" 其后跟随两位的十六进制数来替换。URL 不能包含空格。URL 编码通常使用 + 来替换空格。


| 字符 | URL 编码 |
| :--- | :------- |
| €    | %80      |
| £    | %A3      |
| ©    | %A9      |
| ®    | %AE      |
| À    | %C0      |
| Á    | %C1      |
| Â    | %C2      |
| Ã    | %C3      |
| Ä    | %C4      |
| Å    | %C5      |

[URL 编码参考手册](https://www.w3school.com.cn/tags/html_ref_urlencode.html)。


### 十二、HTML 表单

HTML 表单用于搜集不同类型的用户输入。<form> 元素用于定义 HTML 表单。

```
<form>
 .
form elements
 .
</form>
```

- `<input>` 元素:表单 输入元素

使用的类型：

| 类型   | 描述                                 |
| :----- | :----------------------------------- |
| text   | 定义常规文本输入。                   |
|password|密码字段,加密显示|
| radio  | 定义单选按钮输入（选择多个选择之一） |
|checkbox|定义复选框|
| submit | 定义提交按钮（提交表单）             |
|button| 定义按钮|

设置属性：
| 属性      | 描述                               |
| :-------- | :--------------------------------- |
| disabled  | 规定输入字段应该被禁用。           |
| maxlength | 规定输入字段的最大字符数。         |
| readonly  | 规定输入字段为只读（无法修改）。   |
| size      | 规定输入字段的宽度（以字符计）。   |
| value     | 规定输入字段的默认值。             |

```html
<!DOCTYPE html>
<html>
<body>

<form>
name:<br>
<input type="text" name="name">
<br>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
<br>
<input type="submit" value="Submit">
</form> 

<p>请注意表单本身是不可见的。</p>
<p>同时请注意文本字段的默认宽度是 20 个字符。</p>

</body>
</html>
```

- `<select>`:下拉列表

```html
<!DOCTYPE html>
<html>
<body>

<form action="/demo/demo_form.asp">
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>
<br></br>
<input type="submit">
</form>

</body>
</html>
```

- `<textarea>`: 定义多行输入字段（文本域）

```html
<html>
<body>

<form>
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>
<br><br>
<input type="submit">
</form>

</body>
</html>
```

- `<button>`:定义可点击的按钮
```html
<!DOCTYPE html>
<html>
<body>

<button type="button" onclick="alert('Hello World!')">点击我！</button>

</body>
</html>

```

### 十三、HTML媒体

Web 上的多媒体指的是音效、音乐、视频和动画。

- 视频格式

| 格式      | 文件      | 描述                                                         |
| :-------- | :-------- | :----------------------------------------------------------- |
| AVI       | .avi      | AVI (Audio Video Interleave) 格式是由微软开发的。所有运行 Windows 的计算机都支持 AVI 格式。它是因特网上很常见的格式，但非 Windows 计算机并不总是能够播放。 |
| WMV       | .wmv      | Windows Media 格式是由微软开发的。Windows Media 在因特网上很常见，但是如果未安装额外的（免费）组件，就无法播放 Windows Media 电影。一些后期的 Windows Media 电影在所有非 Windows 计算机上都无法播放，因为没有合适的播放器。 |
| MPEG      | .mpg.mpeg | MPEG (Moving Pictures Expert Group) 格式是因特网上最流行的格式。它是跨平台的，得到了所有最流行的浏览器的支持。 |
| QuickTime | .mov      | QuickTime 格式是由苹果公司开发的。QuickTime 是因特网上常见的格式，但是 QuickTime 电影不能在没有安装额外的（免费）组件的 Windows 计算机上播放。 |
| RealVideo | .rm.ram   | RealVideo 格式是由 Real Media 针对因特网开发的。该格式允许低带宽条件下（在线视频、网络电视）的视频流。由于是低带宽优先的，质量常会降低。 |
| Flash     | .swf.flv  | Flash (Shockwave) 格式是由 Macromedia 开发的。Shockwave 格式需要额外的组件来播放。但是该组件会预装到 Firefox 或 IE 之类的浏览器上。 |
| Mpeg-4    | .mp4      | Mpeg-4 (with H.264 video compression) 是一种针对因特网的新格式。事实上，YouTube 推荐使用 MP4。YouTube 接收多种格式，然后全部转换为 .flv 或 .mp4 以供分发。越来越多的视频发布者转到 MP4，将其作为 Flash 播放器和 HTML5 的因特网共享格式。 |

- 声音格式

| 格式      | 文件      | 描述                                                         |
| :-------- | :-------- | :----------------------------------------------------------- |
| MIDI      | .mid.midi | MIDI (Musical Instrument Digital Interface) 是一种针对电子音乐设备（比如合成器和声卡）的格式。MIDI 文件不含有声音，但包含可被电子产品（比如声卡）播放的数字音乐指令。因为 MIDI 格式仅包含指令，所以 MIDI 文件极其小巧。上面的例子只有 23k 的大小，但却能播放将近 5 分钟。MIDI 得到了广泛的平台上的大量软件的支持。大多数流行的网络浏览器都支持 MIDI。 |
| RealAudio | .rm.ram   | RealAudio 格式是由 Real Media 针对因特网开发的。该格式也支持视频。该格式允许低带宽条件下的音频流（在线音乐、网络音乐）。由于是低带宽优先的，质量常会降低。 |
| Wave      | .wav      | Wave (waveform) 格式是由 IBM 和微软开发的。所有运行 Windows 的计算机和所有网络浏览器（除了 Google Chrome）都支持它。 |
| WMA       | .wma      | WMA 格式 (Windows Media Audio)，质量优于 MP3，兼容大多数播放器，除了 iPod。WMA 文件可作为连续的数据流来传输，这使它对于网络电台或在线音乐很实用。 |
| MP3       | .mp3.mpga | MP3 文件实际上是 MPEG 文件的声音部分。MPEG 格式最初是由运动图像专家组开发的。MP3 是其中最受欢迎的针对音乐的声音格式。期待未来的软件系统都支持它。 |

#### 如何播放


| 标签       | 描述                                         |
| :--------- | :------------------------------------------- |
| `<applet>` | 不赞成。定义内嵌 applet。                    |
| `<embed>`  | HTML4 中不赞成，HTML5 中允许。定义内嵌对象。 |
| `<object>` | 定义内嵌对象。                               |
| `<param>`  | 定义对象的参数。                             |


- `<object>`:使用辅助程序

```html
<!DOCTYPE html>
<html>
<body>

<object width="420" height="360"
 classid="clsid:02BF25D5-8C17-4B23-BC80-D3488ABDDC6B" 
 codebase="http://www.apple.com/qtactivex/qtplugin.cab">
<param name="src" value="/i/bird.wav" />
<param name="controller" value="true" />
</object>

</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<body>

<object width="400" height="40"
classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000"
codebase="http://fpdownload.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=8,0,0,0">
<param name="SRC" value="bookmark.swf">
<embed src="/i/bookmark.swf"></embed>
</object>

</body>
</html>
```

- `<embed>`：定义外部（非 HTML）内容的容器

```html
<!DOCTYPE html>
<html>
<body>

<embed height="100" width="100" src="/i/horse.mp3"></embed>
<p><b>注释：</b>浏览器可能需要安装插件以后，才能播放该文件。</p>

</body>
</html>
```

- `<herf>`:也可以使用超链接,配合js脚本或者辅助应用程序

```html
<!DOCTYPE html>
<html>
<body>

<p><a href="/i/song.mp3">播放 mp3</a></p>
<p><a href="/i/bird.wav">播放 wav</a></p>

<script type="text/javascript" src="http://mediaplayer.yahoo.com/js"></script>

</body>
</html>
```

More info: [HTML 速查手册](https://www.w3school.com.cn/html/html_quick.asp)
[HTML 参考手册](https://www.w3school.com.cn/tags/index.asp)
