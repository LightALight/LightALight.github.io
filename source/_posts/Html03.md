---
title: HTML（三）HTML5
date: 2016-07-15 19:23:32
tags: [web,html]
copyright: true
password:
toc: true
---

HTML5 将成为 HTML、XHTML 以及 HTML DOM 的新标准， 是 W3C 与 WHATWG 合作的结果。 本文章主要介绍 HTML5 的基本概念。

<!--more-->
## Quick Guide



### 一、 声明

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Title of the document</title>
</head>

<body>
Content of the document......
</body>

</html>
```

### 二、浏览器支持

所有现代浏览器都支持 HTML5，都会自动把未识别元素当做行内元素来处理。但是Internet Explorer 8 以及更早的版本，不允许对未知元素添加样式，使用 HTML5 Enabling JavaScript 取解决。

```html
<!DOCTYPE html>
<html>

<head>
  <title>Styling HTML5</title>
  <!--[if lt IE 9]>
  <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
  <![endif]-->
</head>

<body>
<h1>My First Article</h1>

<article>
London is the capital city of England. 
It is the most populous city in the United Kingdom, 
with a metropolitan area of over 13 million inhabitants.
</article>

</body>
</html>
```

### 三、语义元素

| 类型          | 示例                                          |
| :------------ | :-------------------------------------------- |
| Empty         | `<input type="text" value="John Doe" disabled>` |
| Unquoted      | `<input type="text" value=John Doe>`            |
| Double-quoted | `<input type="text" value="John Doe">`          |
| Single-quoted | `<input type="text" value='John Doe'>`         |


### 四、语义元素

HTML5 提供了定义页面不同部分的新语义元素：
![](/image/Html03/ct_sem_elements.png)


| 标签         | 描述                                                 |
| :----------- | :--------------------------------------------------- |
| `<article>`    | 定义文档内的文章。                                   |
| `<aside>`      | 定义页面内容之外的内容。                             |
| `<bdi>`        | 定义与其他文本不同的文本方向。                       |
| `<details>`    | 定义用户可查看或隐藏的额外细节。                     |
| `<dialog>`     | 定义对话框或窗口。                                   |
| `<figcaption>` | 定义 `<figure>` 元素的标题。                           |
| `<figure>`     | 定义自包含内容，比如图示、图表、照片、代码清单等等。 |
| `<footer>`     | 定义文档或节的页脚。                                 |
| `<header>`     | 定义文档或节的页眉。                                 |
| `<main>`       | 定义文档的主内容。                                   |
| `<mark>`       | 定义重要或强调的内容。                               |
| `<menuitem>`   | 定义用户能够从弹出菜单调用的命令/菜单项目。          |
| `<meter>`      | 定义已知范围（尺度）内的标量测量。                   |
| `<nav>`        | 定义文档内的导航链接。                               |
| `<progress>`   | 定义任务进度。                                       |
| `<rp>`         | 定义在不支持 ruby 注释的浏览器中显示什么。           |
| `<rt>`         | 定义关于字符的解释/发音（用于东亚字体）。            |
| `<ruby>`       | 定义 ruby 注释（用于东亚字体）。                     |
| `<section>`    | 定义文档中的节。                                     |
| `<summary>`    | 定义 `<details>` 元素的可见标题。                      |
| `<time>`       | 定义日期/时间。                                      |
| `<wbr>`        | 定义可能的折行（line-break）。                       |


```html
<!DOCTYPE html>
<html>
<body>

<section>
<h1>WWF</h1>
<p>
The World Wide Fund for Nature (WWF) is an international organization working on issues regarding the conservation, research and restoration of the environment, formerly named the World Wildlife Fund. WWF was founded in 1961.
</p>
</section>

<section>
<h1>WWF's Panda symbol</h1>
<p>
The Panda has become the symbol of WWF. The well-known panda logo of WWF originated from a panda named Chi Chi that was transferred from the Beijing Zoo to the London Zoo in the same year of the establishment of WWF.
</p>
</section>

</body>
</html>
```

### 五、图形

- `<canvas>`：使用 JavaScript 在网页上绘制图像。

```html
<!DOCTYPE HTML>
<html>
<body>

<canvas id="myCanvas" width="200" height="100" style="border:1px solid #c3c3c3;">
Your browser does not support the canvas element.
</canvas>

<script type="text/javascript">

var c=document.getElementById("myCanvas");
var cxt=c.getContext("2d");
cxt.fillStyle="#FF0000";
cxt.beginPath();
cxt.arc(70,18,15,0,Math.PI*2,true);
cxt.closePath();
cxt.fill();

</script>

</body>
</html>
```

- `<svg>`:使用 XML 描述 2D 图形的语言

```html
<!DOCTYPE html>
<html>
<body>

<svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
  <polygon points="100,10 40,180 190,60 10,60 160,180"
  style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" />
</svg>

</body>
</html>
```

### 六、媒体

| 标签                       | 描述                                 |
| :----------------------------- | :-------------------- |
| `<audio>`| 标签定义声音，比如音乐或其他音频流。 |
| `<video>`| 标签定义视频。 |
| `<embed>`| 标签定义嵌入的内容，比如插件。       |


- `<video>` 标签的属性

| 属性                  | 值       | 描述                               |
| :------------------------ | :------- | :------------------- |
| [autoplay](https://www.w3school.com.cn/tags/att_video_autoplay.asp) | autoplay | 如果出现该属性，则视频在就绪后马上播放。                     |
| [controls](https://www.w3school.com.cn/tags/att_video_controls.asp) | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| [height](https://www.w3school.com.cn/tags/att_video_height.asp) | *pixels* | 设置视频播放器的高度。                                       |
| [loop](https://www.w3school.com.cn/tags/att_video_loop.asp)  | loop     | 如果出现该属性，则当媒介文件完成播放后再次开始播放。         |
| [preload](https://www.w3school.com.cn/tags/att_video_preload.asp) | preload  | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| [src](https://www.w3school.com.cn/tags/att_video_src.asp)    | *url*    | 要播放的视频的 URL。                                         |
| [width](https://www.w3school.com.cn/tags/att_video_width.asp) | *pixels* | 设置视频播放器的宽度。                                       |

- `<audio>`
```html
<!DOCTYPE HTML>
<html>
<body>

<audio controls="controls">
  <source src="/i/song.ogg" type="audio/ogg">
  <source src="/i/song.mp3" type="audio/mpeg">
Your browser does not support the audio element.
</audio>

</body>
</html>
```

- `<video>`

```html
<!DOCTYPE html>
<html>
<body>

<video width="320" height="240" controls="controls" autoplay="autoplay">
  <source src="/i/movie.ogg" type="video/ogg" />
  <source src="/i/movie.mp4" type="video/mp4" />
  <source src="/i/movie.webm" type="video/webm" />
</video>

</body>
</html>
```

### 七、API

#### 地理位置

getCurrentPosition():获得用户的地理位置


| 返回对象的属性                    | 描述                   |
| :---------------------- | :--------------------- |
| coords.latitude         | 十进制数的纬度         |
| coords.longitude        | 十进制数的经度         |
| coords.accuracy         | 位置精度               |
| coords.altitude         | 海拔，海平面以上以米计 |
| coords.altitudeAccuracy | 位置的海拔精度         |
| coords.heading          | 方向，从正北开始以度计 |
| coords.speed            | 速度，以米/每秒计      |
| timestamp               | 响应的日期/时间        |


```html
<!DOCTYPE html>
<html>
<body>
<p id="demo">点击这个按钮，获得您的坐标：</p>
<button onclick="getLocation()">试一下</button>
<script>
var x=document.getElementById("demo");
function getLocation()
  {
  if (navigator.geolocation)
    {
    navigator.geolocation.getCurrentPosition(showPosition,showError);
    }
  else{x.innerHTML="Geolocation is not supported by this browser.";}
  }
function showPosition(position)
  {
  x.innerHTML="Latitude: " + position.coords.latitude + 
  "<br />Longitude: " + position.coords.longitude;	
  }
function showError(error)
  {
  switch(error.code) 
    {
    case error.PERMISSION_DENIED:
      x.innerHTML="User denied the request for Geolocation."
      break;
    case error.POSITION_UNAVAILABLE:
      x.innerHTML="Location information is unavailable."
      break;
    case error.TIMEOUT:
      x.innerHTML="The request to get user location timed out."
      break;
    case error.UNKNOWN_ERROR:
      x.innerHTML="An unknown error occurred."
      break;
    }
  }
</script>
</body>
</html>
```



#### 拖放

- 把元素设置为可拖放:draggable="true"
- 拖放的内容:ondragstart 规定拖动什么数据。,dataTransfer.setData()设置拖动数据的数据类型和值
- 拖到何处:ondragover规定被拖动的数据能够被放置到何处
- 进行放置:ondrop

```html
<!DOCTYPE HTML>
<html>
<head>
<style type="text/css">
#div1, #div2
{float:left; width:198px; height:66px; margin:10px;padding:10px;border:1px solid #aaaaaa;}
</style>
<script type="text/javascript">
function allowDrop(ev)
{
ev.preventDefault();
}

function drag(ev)
{
ev.dataTransfer.setData("Text",ev.target.id);
}

function drop(ev)
{
<!-- 调用 preventDefault() 来阻止数据的浏览器默认处理方式（drop 事件的默认行为是以链接形式打开） -->
ev.preventDefault();
<!-- 通过 dataTransfer.getData() 方法获得被拖的数据。该方法将返回在 setData() 方法中设置为相同类型的任何数据 -->
var data=ev.dataTransfer.getData("Text");
<!-- 被拖数据是被拖元素的 id ("drag1"),把被拖元素追加到放置元素中 -->
ev.target.appendChild(document.getElementById(data));
}
</script>
</head>
<body>

<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
  <img src="/i/eg_dragdrop_w3school.gif" draggable="true" ondragstart="drag(event)" id="drag1" />
</div>
<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>

</body>
</html>
```

#### 应用程序缓存

HTML5 引入了应用程序缓存，这意味着 web 应用可进行缓存，并可在没有因特网连接时进行访问。通过创建 cache manifest 文件，可以轻松地创建 web 应用的离线版本。

应用程序缓存为应用带来三个优势：
- 离线浏览 - 用户可在应用离线时使用它们
- 速度 - 已缓存资源加载得更快
- 减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。

- 浏览器支持：所有主流浏览器均支持应用程序缓存，除了 Internet Explorer。


- 样例
```html
<!DOCTYPE HTML>
<html manifest="demo.appcache">

<body>
The content of the document......
</body>

</html>
```

**请注意，manifest 文件需要配置正确的 MIME-type，即 "text/cache-manifest"。必须在 web 服务器上进行配置。**


manifest 文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。manifest 文件可分为三个部分：

- CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存

```html
CACHE MANIFEST
/theme.css
/logo.gif
/main.js
```
- NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存

```
NETWORK:
login.asp
```
```
NETWORK:
*
```
- FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）


```html
FALLBACK:
/html5/ /404.html
```


- 更新缓存:一旦应用被缓存，它就会保持缓存直到发生下列情况
    - 用户清空浏览器缓存
    - manifest 文件被修改
    - 由程序来更新应用缓存


**重要的提示：如果您编辑了一幅图片，或者修改了一个 JavaScript 函数，这些改变都不会被重新缓存。以 "#" 开头的是注释行，更新注释行中的日期和版本号是一种使浏览器重新缓存文件的办法。**


#### Web Workers

当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行。

浏览器支持：所有主流浏览器均支持 web worker，除了 Internet Explorer。

- 1.创建 web worker 文件：demo_workers.js

```javascript
var i=0;

function timedCount()
{
i=i+1;
postMessage(i);
setTimeout("timedCount()",500);
}

timedCount();
```

- 2.创建 Web Worker 对象

```html
<!DOCTYPE html>
<html>
<body>

<p>计数: <output id="result"></output></p>
<button onclick="startWorker()">开始 Worker</button> 
<button onclick="stopWorker()">停止 Worker</button>
<br /><br />

<script>
var w;

function startWorker()
{
// 检测用户的浏览器是否支持它
if(typeof(Worker)!=="undefined")
  {
  if(typeof(w)=="undefined")
  {
  // 创建 Web Worker 对象
  w=new Worker("/example/html5/demo_workers.js");
  }
  w.onmessage = function (event) {
    document.getElementById("result").innerHTML=event.data;
    };
  }
else
  {
  document.getElementById("result").innerHTML="Sorry, your browser does not support Web Workers...";
  }
}
// 终止 Web Worker
function stopWorker()
{ 
w.terminate();
}
</script>

</body>
</html>
```



#### 服务器发送事件

服务器发送事件（server-sent event）允许网页获得来自服务器的更新。

- 浏览器支持：所有主流浏览器均支持服务器发送事件，除了 Internet Explorer。

- 1.创建服务器端实例:把 "Content-Type" 报头设置为 "text/event-stream".

demo_sse.php
```php
<?php
header('Content-Type: text/event-stream');
header('Cache-Control: no-cache');

$time = date('r');
echo "data: The server time is: {$time}\n\n";
flush();
?>
```
demo_sse.asp
```asp
<%
Response.ContentType="text/event-stream"
Response.Expires=-1
Response.Write("data: " & now())
Response.Flush()
%>
```

- 2.创建Server-Sent 事件
```html
<!DOCTYPE html>
<html>
<body>
<h1>获得服务器更新</h1>
<div id="result"></div>

<script>
// 检测服务器发送事件的浏览器支持情况
if(typeof(EventSource)!=="undefined")
  {
  // 接收 Server-Sent 事件通知
  var source=new EventSource("/example/html5/demo_sse.php");
  source.onmessage=function(event)
    {
    document.getElementById("result").innerHTML+=event.data + "<br />";
    };
  }
else
  {
  document.getElementById("result").innerHTML="抱歉，您的浏览器不支持 server-sent 事件 ...";
  }
</script>

</body>
</html>
```

在上面的例子中，我们使用 onmessage 事件来获取消息。不过还可以使用其他事件：

| 事件      | 描述                     |
| :-------- | :----------------------- |
| onopen    | 当通往服务器的连接被打开 |
| onmessage | 当接收到消息             |
| onerror   | 当错误发生               |

### 八、表单

HTML 表单用于搜集不同类型的用户输入。`<form>` 元素用于定义 HTML 表单。

```html
<form>
 .
form elements
 .
</form>
```

- `<input>` 元素:表单 输入元素

新增类型：

| 类型   | 描述                                 |
| :----- | :----------------------------------- |
|color|设置输入类型为颜色|
|date|设置输入类型为日期|
|datetime|设置输入类型为日期和时间（有时区）|
|datetime-local|设置输入类型为日期和时间（无时区）|
|email|设置输入类型为邮箱，被提交时自动对电子邮件地址进行验证|
|month|设置输入类型为年月|
|number|设置输入类型为数字|
|range|设置输入类型为一定范围内的值，配合属性来规定限制：min、max、step、value|
|search|设置输入类型为搜索|
|tel|设置输入类型为电话|
|time|设置输入类型为时间（无时区）|
|url|设置输入类型为网站，提交时能够自动验证|
|week|设置输入类型为周和年|


新增设置属性：

| 属性      | 描述                               |
| :-------- | :--------------------------------- |
| autocomplete      |  规定form 或 input 域的自动完成：提交表单，重新加载|
| autofocus         | 规定 页面加载时，input 域 自动地获得焦点 |
| form              |  规定 input 域 所属的一个或多个表单  |
| form overrides    |   规定 input 域 的表单重写属性 |
| height and width  |   规定 input 域 的高度和宽度 |
| list              |  规定 input 域 的的选项列表 |
| min, max and step | 规定 input 域 的最大、最小、数字间隔    |
| multiple          |  规定 input 域 中可选择多个值 |
| novalidate        |  规定在提交表单时不应该验证 form 或 input 域|
| pattern           | 规定检查 input 域 是否满足正则表达式。 |
| placeholder       |   提供一种提示（hint），描述 input 域 所期待的值|
| required          | 规定 input 域 是必需的（必需填写）。 |



```html
<!DOCTYPE HTML>
<html>
<body>

<form action="/example/html5/demo_form.asp" method="get" autocomplete="on">
First name:<input type="text" name="fname" /><br />
Last name: <input type="text" name="lname" /><br />
E-mail: <input type="email" name="email" autocomplete="off" /><br />
<input type="submit" />
</form>

<p>请填写并提交此表单，然后重载页面，来查看自动完成功能是如何工作的。</p>
<p>请注意，表单的自动完成功能是打开的，而 e-mail 域是关闭的。</p>

</body>
</html>
```

#### 新的表单元素

| 标签       | 描述                             |
| :--------- | :------------------------------- |
| `<datalist>` | 定义输入控件的预定义选项。       |
| `<keygen>`   | 定义键对生成器字段（用于表单）。 |
| `<output>`   | 定义计算结果。                   |



- `<datalist>` :为 `<input>` 元素规定预定义选项列表。元素的 list 属性必须引用 `<datalist>` 元素的 id 属性。

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
<br><br>
<input type="submit">
</form>

</body>
</html>
```

- `<keygen >`:密钥对生成器（key-pair generator）。当提交表单时，会生成两个键，一个是私钥，一个公钥。私钥（private key）存储于客户端，公钥（public key）则被发送到服务器。公钥可用于之后验证用户的客户端证书（client certificate）。

```html
<!DOCTYPE HTML>
<html>
<body>

<form action="/example/html5/demo_form.asp" method="get">
Username: <input type="text" name="usr_name" />
Encryption: <keygen name="security" />
<input type="submit" />
</form>

</body>
</html>
```

- `<output >`:用于不同类型的输出

```html
<!DOCTYPE HTML>
<html>
<head>
<script type="text/javascript">
function resCalc()
{
numA=document.getElementById("num_a").value;
numB=document.getElementById("num_b").value;
document.getElementById("result").value=Number(numA)+Number(numB);
}
</script>
</head>
<body>
<p>使用 output 元素的简易计算器：</p>
<form onsubmit="return false">
 <input id="num_a" /> +
 <input id="num_b" /> =
 <output id="result" onforminput="resCalc()"></output>
</form>

</body>
</html>
```

### 九、HTML5 迁移


#### 元素切换

|     典型的 HTML4     | 典型的 HTML5 |
| :------------------: | :----------: |
| `<div id="header">`  |  `<header>`  |
|  `<div id="menu">`   |   `<nav>`    |
| `<div id="content">` | `<section>`  |
|  `<div id="post">`   | `<article>`  |
| `<div id="footer">`  |  `<footer>`  |

#### 更改Doctype

```html
<!DOCTYPE html>
```

#### 更改编码

```html
<meta charset="utf-8">
```

#### 添加 shiv

```html
<!--[if lt IE 9]>
  <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->
```

#### 为语义元素添加 CSS


### 代码规范

- 请使用正确的文档类型
- 请使用小写元素名
- 关闭所有 HTML 元素
- 关闭空的 HTML 元素
- 使用小写属性名
- 属性值加引号：属性值有空格需要引号
- 必需的属性：始终对图像使用 alt 属性
- 空格和等号：等号两边不要空格
- 避免长代码行：代码行超过 80 个字符
- 空行和缩进：请勿使用没有必要的空行和缩进。没有必要在短的和相关项目之间使用空行，也没有必要缩进每个元素
- 不推荐省略 `<html>` 和 `<body>` 标签。
- `<title>`是必须的
- 注释规范:短注释应该在单行中书写，并在 <!-- 之后增加一个空格，在 <!-- 之前增加一个空格;长注释，跨越多行，应该通过 <!-- 和 --> 在独立的行中书写
- 请使用简单的语法来链接样式表
	- 开括号与选择器位于同一行
	- 在开括号之前用一个空格
	- 使用两个字符的缩进
	- 在每个属性与其值之间使用冒号加一个空格
	- 在每个逗号或分号之后使用空格
	- 在每个属性值对（包括最后一个）之后使用分号
	- 只在值包含空格时使用引号来包围值
	- 把闭括号放在新的一行，之前不用空格
	- 避免每行超过 80 个字符 	
- 使用简单的语法来加载外部脚本
- 在 HTML 中使用（与 JavaScript）相同的命名约定
- 使用小写文件名
- 文件扩展名要规范：html文件 .html; css文件 .css ;JavaScript .js