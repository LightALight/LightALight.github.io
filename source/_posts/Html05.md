---
title: HTML（五）CSS3
date: 2016-09-15 19:23:32
tags: [web,html]
copyright: true
password:
toc: true
---

CSS3 是最新的 CSS 标准。本文章主要介绍 CSS3 的基本概念。

<!--more-->

## Quick Guide

CSS3 完全向后兼容，因此您不必改变现有的设计。浏览器通常支持 CSS2。

### 一、边框

创建圆角边框，向矩形添加阴影，使用图片来绘制边框.

| 属性                                                         | 描述                                          | CSS  |
| :----------------------------------------------------------- | :-------------------------------------------- | :--- |
| [border-image](https://www.w3school.com.cn/cssref/pr_border-image.asp) | 设置所有 border-image-* 属性的简写属性。      | 3    |
| [border-radius](https://www.w3school.com.cn/cssref/pr_border-radius.asp) | 设置所有四个 border-*-radius 属性的简写属性。 | 3    |
| [box-shadow](https://www.w3school.com.cn/cssref/pr_box-shadow.asp) | 向方框添加一个或多个阴影。                    | 3    |

- border-radius:圆角边框
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
text-align:center;
border:2px solid #a1a1a1;
padding:10px 40px; 
background:#dddddd;
width:350px;
border-radius:25px;
-moz-border-radius:25px; /* 老的 Firefox */
}
</style>
</head>
<body>

<div>border-radius 属性允许您向元素添加圆角。</div>

</body>
</html>
```

- box-shadow:边框阴影
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:300px;
height:100px;
background-color:#ff9900;
-moz-box-shadow: 10px 10px 5px #888888; /* 老的 Firefox */
box-shadow: 10px 10px 5px #888888;
}
</style>
</head>
<body>

<div></div>

</body>
</html>
```

- border-image:边框图片

```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
border:15px solid transparent;
width:300px;
padding:10px 20px;
}

#round
{
-moz-border-image:url(/i/border.png) 30 30 round;	/* Old Firefox */
-webkit-border-image:url(/i/border.png) 30 30 round;	/* Safari and Chrome */
-o-border-image:url(/i/border.png) 30 30 round;		/* Opera */
border-image:url(/i/border.png) 30 30 round;
}

#stretch
{
-moz-border-image:url(/i/border.png) 30 30 stretch;	/* Old Firefox */
-webkit-border-image:url(/i/border.png) 30 30 stretch;	/* Safari and Chrome */
-o-border-image:url(/i/border.png) 30 30 stretch;	/* Opera */
border-image:url(/i/border.png) 30 30 stretch;
}
</style>
</head>
<body>

<div id="round">在这里，图片铺满整个边框。</div>
<br>
<div id="stretch">在这里，图片被拉伸以填充该区域。</div>

<p>这是我们使用的图片：</p>
<img src="/i/border.png">

<p><b>注释：</b> Internet Explorer 不支持 border-image 属性。</p>
<p>border-image 属性规定了用作边框的图片。</p>

</body>
</html>
```

### 二、背景

- background-size:规定背景图片的尺寸

```html
<!DOCTYPE html>
<html>
<head>
<style> 
body
{
background:url(/i/bg_flower.gif);
background-size:63px 100px;
-moz-background-size:63px 100px; /* 老版本的 Firefox */
background-repeat:no-repeat;
padding-top:80px;
}
</style>
</head>

<body>
<p>上面是缩小的背景图片。</p>

<p>原始图片：<img src="/i/bg_flower.gif" alt="Flowers"></p>

</body>
</html>
```

- background-origin:规定背景图片的定位区域

```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
border:1px solid black;
padding:35px;
background-image:url('/i/bg_flower.gif');
background-repeat:no-repeat;
background-position:left;
}
#div1
{
background-origin:border-box;
}
#div2
{
background-origin:content-box;
}
</style>
</head>
<body>

<p>background-origin:border-box:</p>
<div id="div1">
这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。
</div>

<p>background-origin:content-box:</p>
<div id="div2">
这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。
</div>

</body>
</html>
```

- background-image:使用多个背景图像
```html
<!DOCTYPE html>
<html>
<head>
<style> 
body
{
background-image:url(/i/bg_flower.gif),url(/i/bg_flower_2.gif);
}
</style>
</head>
<body>

</body>
</html>
```

### 三、文本效果

| 属性                                                         | 描述                                                    | CSS  |
| :----------------------------------------------------------- | :------------------------------------------------------ | :--- |
| [hanging-punctuation](https://www.w3school.com.cn/cssref/pr_hanging-punctuation.asp) | 规定标点字符是否位于线框之外。                          | 3    |
| [punctuation-trim](https://www.w3school.com.cn/cssref/pr_punctuation-trim.asp) | 规定是否对标点字符进行修剪。                            | 3    |
| text-align-last                                              | 设置如何对齐最后一行或紧挨着强制换行符之前的行。        | 3    |
| [text-emphasis](https://www.w3school.com.cn/cssref/pr_text-emphasis.asp) | 向元素的文本应用重点标记以及重点标记的前景色。          | 3    |
| [text-justify](https://www.w3school.com.cn/cssref/pr_text-justify.asp) | 规定当 text-align 设置为 "justify" 时所使用的对齐方法。 | 3    |
| [text-outline](https://www.w3school.com.cn/cssref/pr_text-outline.asp) | 规定文本的轮廓。                                        | 3    |
| [text-overflow](https://www.w3school.com.cn/cssref/pr_text-overflow.asp) | 规定当文本溢出包含元素时发生的事情。                    | 3    |
| [text-shadow](https://www.w3school.com.cn/cssref/pr_text-shadow.asp) | 向文本添加阴影。                                        | 3    |
| [text-wrap](https://www.w3school.com.cn/cssref/pr_text-wrap.asp) | 规定文本的换行规则。                                    | 3    |
| [word-break](https://www.w3school.com.cn/cssref/pr_word-break.asp) | 规定非中日韩文本的换行规则。                            | 3    |
| [word-wrap](https://www.w3school.com.cn/cssref/pr_word-wrap.asp) | 允许对长的不可分割的单词进行分割并换行到下一行。        | 3    |

-  text-shadow 可向文本应用阴影 

```html
<!DOCTYPE html>
<html>
<head>
<style>
h1
{
text-shadow: 5px 5px 5px #FF0000;
}
</style>
</head>
<body>

<h1>文本阴影效果！</h1>

</body>
</html>
```

-  word-wrap 属性允许您允许文本强制文本进行换行 - 即使这意味着会对单词进行拆分：

```html
<!DOCTYPE html>
<html>
<head>
<style> 
p.test
{
width:11em; 
border:1px solid #000000;
word-wrap:break-word;
}
</style>
</head>
<body>

<p class="test">This paragraph contains a very long word: thisisaveryveryveryveryveryverylongword. The long word will break and wrap to the next line.</p>

</body>
</html>
```

  

### 四、字体

在 CSS3 之前，web 设计师必须使用已在用户计算机上安装好的字体。

通过 CSS3，web 设计师可以使用他们喜欢的任意字体。将该字体文件存放到 web 服务器上，它会在需要时被自动下载到用户的计算机上。字体是通过 CSS3 @font-face 规则中定义的。

```html
<!DOCTYPE html>
<html>
<head>
<style> 
@font-face
{
font-family: myFirstFont;/* 定义字体的名称 */
src: url('/example/css3/Sansation_Light.ttf') /* 指向字体文件 */
    ,url('/example/css3/Sansation_Light.eot'); /* IE9+ */
}

@font-face
{
font-family: myFirstFont;
src: url('/example/css3/Sansation_Bold.ttf')
    ,url('/example/css3/Sansation_Bold.eot'); /* IE9+ */
font-weight:bold;
}

div
{
font-family:myFirstFont;
}
</style>
</head>
<body>

<div>
With CSS3, websites can <b>finally</b> use fonts other than the pre-selected "web-safe" fonts.
</div>

<p><b>注释：</b>Internet Explorer 9+ 支持新的 @font-face 规则。Internet Explorer 8 以及更早的版本不支持新的 @font-face 规则。</p>

</body>
</html>
```

下面的表格列出了能够在 @font-face 规则中定义的所有字体描述符：

| 描述符        | 值          | 描述                        |
| :------------ | :------------------------ | :--------------------- |
| font-family   | *name*                                                       | 必需。规定字体的名称。                                       |
| src           | *URL*                                                        | 必需。定义字体文件的 URL。                                   |
| font-stretch  | normalcondensedultra-condensedextra-condensedsemi-condensedexpandedsemi-expandedextra-expandedultra-expanded | 可选。定义如何拉伸字体。默认是 "normal"。                    |
| font-style    | ormalitalicoblique                                           | 可选。定义字体的样式。默认是 "normal"。                      |
| font-weight   | normalbold100200300400500600700800900                        | 可选。定义字体的粗细。默认是 "normal"。                      |
| unicode-range | *unicode-range*                                              | 可选。定义字体支持的 UNICODE 字符范围。默认是 "U+0-10FFFF"。 |



### 五、转换

 转换是使元素改变形状、尺寸和位置的一种效果。 

- 2D 转换

| 转换属性                                                     | 描述                         | CSS  |
| :----------------------------------------------------------- | :--------------------------- | :--- |
| [transform](https://www.w3school.com.cn/cssref/pr_transform.asp) | 向元素应用 2D 或 3D 转换。   | 3    |
| [transform-origin](https://www.w3school.com.cn/cssref/pr_transform-origin.asp) | 允许你改变被转换元素的位置。 | 3    |

| 2D转换函数                      | 描述                                     |
| :------------------------------ | :--------------------------------------- |
| matrix(*n*,*n*,*n*,*n*,*n*,*n*) | 定义 2D 转换，使用六个值的矩阵。         |
| translate(*x*,*y*)              | 定义 2D 转换，沿着 X 和 Y 轴移动元素。   |
| translateX(*n*)                 | 定义 2D 转换，沿着 X 轴移动元素。        |
| translateY(*n*)                 | 定义 2D 转换，沿着 Y 轴移动元素。        |
| scale(*x*,*y*)                  | 定义 2D 缩放转换，改变元素的宽度和高度。 |
| scaleX(*n*)                     | 定义 2D 缩放转换，改变元素的宽度。       |
| scaleY(*n*)                     | 定义 2D 缩放转换，改变元素的高度。       |
| rotate(*angle*)                 | 定义 2D 旋转，在参数中规定角度。         |
| skew(*x-angle*,*y-angle*)       | 定义 2D 倾斜转换，沿着 X 和 Y 轴。       |
| skewX(*angle*)                  | 定义 2D 倾斜转换，沿着 X 轴。            |
| skewY(*angle*)                  | 定义 2D 倾斜转换，沿着 Y 轴。            |

```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:75px;
background-color:yellow;
border:1px solid black;
}
div#div2
{
transform:matrix(0.866,0.5,-0.5,0.866,0,0);
-ms-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* IE 9 */
-moz-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* Firefox */
-webkit-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* Safari and Chrome */
-o-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* Opera */
}
</style>
</head>
<body>

<div>你好。这是一个 div 元素。</div>

<div id="div2">你好。这是一个 div 元素。</div>

</body>
</html>
```


- 3D 转换

| 转换属性                                                     | 描述                                 | CSS  |
| :----------------------------------------------------------- | :----------------------------------- | :--- |
| [transform](https://www.w3school.com.cn/cssref/pr_transform.asp) | 向元素应用 2D 或 3D 转换。           | 3    |
| [transform-origin](https://www.w3school.com.cn/cssref/pr_transform-origin.asp) | 允许你改变被转换元素的位置。         | 3    |
| [transform-style](https://www.w3school.com.cn/cssref/pr_transform-style.asp) | 规定被嵌套元素如何在 3D 空间中显示。 | 3    |
| [perspective](https://www.w3school.com.cn/cssref/pr_perspective.asp) | 规定 3D 元素的透视效果。             | 3    |
| [perspective-origin](https://www.w3school.com.cn/cssref/pr_perspective-origin.asp) | 规定 3D 元素的底部位置。             | 3    |
| [backface-visibility](https://www.w3school.com.cn/cssref/pr_backface-visibility.asp) | 定义元素在不面对屏幕时是否可见。     | 3    |

| 3D转换函数                                                   | 描述                                      |
| :----------------------------------------------------------- | :---------------------------------------- |
| matrix3d(*n*,*n*,*n*,*n*,*n*,*n*, *n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*) | 定义 3D 转换，使用 16 个值的 4x4 矩阵。   |
| translate3d(*x*,*y*,*z*)                                     | 定义 3D 转化。                            |
| translateX(*x*)                                              | 定义 3D 转化，仅使用用于 X 轴的值。       |
| translateY(*y*)                                              | 定义 3D 转化，仅使用用于 Y 轴的值。       |
| translateZ(*z*)                                              | 定义 3D 转化，仅使用用于 Z 轴的值。       |
| scale3d(*x*,*y*,*z*)                                         | 定义 3D 缩放转换。                        |
| scaleX(*x*)                                                  | 定义 3D 缩放转换，通过给定一个 X 轴的值。 |
| scaleY(*y*)                                                  | 定义 3D 缩放转换，通过给定一个 Y 轴的值。 |
| scaleZ(*z*)                                                  | 定义 3D 缩放转换，通过给定一个 Z 轴的值。 |
| rotate3d(*x*,*y*,*z*,*angle*)                                | 定义 3D 旋转。                            |
| rotateX(*angle*)                                             | 定义沿 X 轴的 3D 旋转。                   |
| rotateY(*angle*)                                             | 定义沿 Y 轴的 3D 旋转。                   |
| rotateZ(*angle*)                                             | 定义沿 Z 轴的 3D 旋转。                   |
| perspective(*n*)                                             | 定义 3D 转换元素的透视视图。              |

```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:75px;
background-color:yellow;
border:1px solid black;
}
div#div2
{
transform:rotateY(130deg);
-webkit-transform:rotateY(130deg); /* Safari and Chrome */
-moz-transform:rotateY(130deg); /* Firefox */
}
</style>
</head>
<body>

<div>你好。这是一个 div 元素。</div>

<div id="div2">你好。这是一个 div 元素。</div>

<p><b>注释：</b> Internet Explorer 和 Opera 不支持 rotateX 方法。</p>

</body>
</html>
```

### 六、过渡

过渡是元素从一种样式逐渐改变为另一种的效果。

要实现这一点，必须规定两项内容：

- 规定您希望把效果添加到哪个 CSS 属性上
- 规定效果的时长

| 转换属性                                                     | 描述                                         | CSS  |
| :----------------------------------------------------------- | :------------------------------------------- | :--- |
| [transition](https://www.w3school.com.cn/cssref/pr_transition.asp) | 简写属性，用于在一个属性中设置四个过渡属性。 | 3    |
| [transition-property](https://www.w3school.com.cn/cssref/pr_transition-property.asp) | 规定应用过渡的 CSS 属性的名称。              | 3    |
| [transition-duration](https://www.w3school.com.cn/cssref/pr_transition-duration.asp) | 定义过渡效果花费的时间。默认是 0。           | 3    |
| [transition-timing-function](https://www.w3school.com.cn/cssref/pr_transition-timing-function.asp) | 规定过渡效果的时间曲线。默认是 "ease"。      | 3    |
| [transition-delay](https://www.w3school.com.cn/cssref/pr_transition-delay.asp) | 规定过渡效果何时开始。默认是 0。             | 3    |



```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
/* 过渡前 */
width:100px;
height:100px;
background:yellow;
transition:width 2s, height 2s;
-moz-transition:width 2s, height 2s, -moz-transform 2s; /* Firefox 4 */
-webkit-transition:width 2s, height 2s, -webkit-transform 2s; /* Safari and Chrome */
-o-transition:width 2s, height 2s, -o-transform 2s; /* Opera */
}

div:hover
{
/* 过渡后 */
width:200px;
height:200px;
transform:rotate(180deg);
-moz-transform:rotate(180deg); /* Firefox 4 */
-webkit-transform:rotate(180deg); /* Safari and Chrome */
-o-transform:rotate(180deg); /* Opera */
}
</style>
</head>
<body>

<div>请把鼠标指针放到黄色的 div 元素上，来查看过渡效果。</div>

<p><b>注释：</b>本例在 Internet Explorer 中无效。</p>

</body>
</html>
```



### 七、动画

动画是使元素从一种样式逐渐变化为另一种样式的效果。

请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%。

0% 是动画的开始，100% 是动画的完成。

为了得到最佳的浏览器支持，您应该始终定义 0% 和 100% 选择器。

当您在 @keyframes 中创建动画时，请把它捆绑到某个选择器，否则不会产生动画效果。

通过规定至少以下两项 CSS3 动画属性，即可将动画绑定到选择器：

- 规定动画的名称
- 规定动画的时长

| 动画属性                                                        | 描述                                                     | CSS  |
| :----------------------------------------------------------- | :------------------------------------------------------- | :--- |
| [@keyframes](https://www.w3school.com.cn/cssref/pr_keyframes.asp) | 规定动画。                                               | 3    |
| [animation](https://www.w3school.com.cn/cssref/pr_animation.asp) | 所有动画属性的简写属性，除了 animation-play-state 属性。 | 3    |
| [animation-name](https://www.w3school.com.cn/cssref/pr_animation-name.asp) | 规定 @keyframes 动画的名称。                             | 3    |
| [animation-duration](https://www.w3school.com.cn/cssref/pr_animation-duration.asp) | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。         | 3    |
| [animation-timing-function](https://www.w3school.com.cn/cssref/pr_animation-timing-function.asp) | 规定动画的速度曲线。默认是 "ease"。                      | 3    |
| [animation-delay](https://www.w3school.com.cn/cssref/pr_animation-delay.asp) | 规定动画何时开始。默认是 0。                             | 3    |
| [animation-iteration-count](https://www.w3school.com.cn/cssref/pr_animation-iteration-count.asp) | 规定动画被播放的次数。默认是 1。                         | 3    |
| [animation-direction](https://www.w3school.com.cn/cssref/pr_animation-direction.asp) | 规定动画是否在下一周期逆向地播放。默认是 "normal"。      | 3    |
| [animation-play-state](https://www.w3school.com.cn/cssref/pr_animation-play-state.asp) | 规定动画是否正在运行或暂停。默认是 "running"。           | 3    |
| [animation-fill-mode](https://www.w3school.com.cn/cssref/pr_animation-fill-mode.asp) | 规定对象动画时间之外的状态。                             | 3    |


```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:100px;
background:red;
position:relative;
animation-name:myfirst;
animation-duration:5s;
animation-timing-function:linear;
animation-delay:2s;
animation-iteration-count:infinite;
animation-direction:alternate;
animation-play-state:running;
/* Firefox: */
-moz-animation-name:myfirst;
-moz-animation-duration:5s;
-moz-animation-timing-function:linear;
-moz-animation-delay:2s;
-moz-animation-iteration-count:infinite;
-moz-animation-direction:alternate;
-moz-animation-play-state:running;
/* Safari and Chrome: */
-webkit-animation-name:myfirst;
-webkit-animation-duration:5s;
-webkit-animation-timing-function:linear;
-webkit-animation-delay:2s;
-webkit-animation-iteration-count:infinite;
-webkit-animation-direction:alternate;
-webkit-animation-play-state:running;
/* Opera: */
-o-animation-name:myfirst;
-o-animation-duration:5s;
-o-animation-timing-function:linear;
-o-animation-delay:2s;
-o-animation-iteration-count:infinite;
-o-animation-direction:alternate;
-o-animation-play-state:running;
}

@keyframes myfirst
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

@-moz-keyframes myfirst /* Firefox */
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

@-webkit-keyframes myfirst /* Safari and Chrome */
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

@-o-keyframes myfirst /* Opera */
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}
</style>
</head>
<body>

<p><b>注释：</b>本例在 Internet Explorer 中无效。</p>

<div></div>

</body>
</html>
```

### 八、多列

 创建多个列来对文本进行布局 

| 属性                                                         | 描述                                               | CSS  |
| :----------------------------------------------------------- | :------------------------------------------------- | :--- |
| [column-count](https://www.w3school.com.cn/cssref/pr_column-count.asp) | 规定元素应该被分隔的列数。                         | 3    |
| [column-fill](https://www.w3school.com.cn/cssref/pr_column-fill.asp) | 规定如何填充列。                                   | 3    |
| [column-gap](https://www.w3school.com.cn/cssref/pr_column-gap.asp) | 规定列之间的间隔。                                 | 3    |
| [column-rule](https://www.w3school.com.cn/cssref/pr_column-rule.asp) | 设置所有 column-rule-* 属性的简写属性。            | 3    |
| [column-rule-color](https://www.w3school.com.cn/cssref/pr_column-rule-color.asp) | 规定列之间规则的颜色。                             | 3    |
| [column-rule-style](https://www.w3school.com.cn/cssref/pr_column-rule-style.asp) | 规定列之间规则的样式。                             | 3    |
| [column-rule-width](https://www.w3school.com.cn/cssref/pr_column-rule-width.asp) | 规定列之间规则的宽度。                             | 3    |
| [column-span](https://www.w3school.com.cn/cssref/pr_column-span.asp) | 规定元素应该横跨的列数。                           | 3    |
| [column-width](https://www.w3school.com.cn/cssref/pr_column-width.asp) | 规定列的宽度。                                     | 3    |
| [columns](https://www.w3school.com.cn/cssref/pr_columns.asp) | 规定设置 column-width 和 column-count 的简写属性。 | 3    |

```html
<!DOCTYPE html>
<html>
<head>
<style> 
.newspaper
{
-moz-column-count:3; /* Firefox */
-webkit-column-count:3; /* Safari and Chrome */
column-count:3;

-moz-column-gap:40px; /* Firefox */
-webkit-column-gap:40px; /* Safari and Chrome */
column-gap:40px;

-moz-column-rule:4px outset #ff0000; /* Firefox */
-webkit-column-rule:4px outset #ff0000; /* Safari and Chrome */
column-rule:4px outset #ff0000;
}
</style>
</head>
<body>

<p><b>注释：</b>Internet Explorer 不支持 column-count 属性。</p>

<div class="newspaper">
人民网北京2月24日电 (记者 刘阳)国家发展改革委近日发出通知，决定自2月25日零时起将汽、柴油价格每吨分别提高300元和290元，折算到90号汽油和0号柴油（全国平均）每升零售价格分别提高0.22元和0.25元。

此次国内成品油价格调整幅度，是按照现行国内成品油价格形成机制，根据国际市场油价变化情况确定的。去年11月16日国内成品油价格调整以来，受市场预期欧美经济复苏前景向好以及中东局势持续动荡等因素影响，国际市场原油价格先抑后扬，2月上旬WTI和布伦特原油期货价格再次回升至每桶95美元和115美元以上。虽然近两日价格有所回落，但国内油价挂钩的国际市场三种原油连续22个工作日移动平均价格上涨幅度已超过4%，达到国内成品油价格调整的边界条件。

通知指出，这次成品油调价后，国家将按照已建立的补贴机制，继续对种粮农民、渔业（含远洋渔业）、林业、城市公交、农村道路客运（含岛际和农村水路客运）等给予补贴。同时，为保证市场物价基本稳定，防止连锁涨价，对与居民生活密切相关的铁路客运、城市公交、农村道路客运（含岛际和农村水路客运）价格不作调整。

通知要求，中石油、中石化、中海油三大公司要组织好成品油生产和调运，保持合理库存，加强综合协调和应急调度，保障成品油供应。各级价格主管部门要加大市场监督检查力度，依法查处不执行国家价格政策，以及囤积居奇、造谣惑众、合谋涨价、搭车涨价等违法行为，维护正常市场秩序。
</div>

</body>
</html>
```



### 九、用户界面

 用户界面特性包括重设元素尺寸、盒尺寸以及轮廓等。 

| 属性                                                         | 描述                                               | CSS  |
| :----------------------------------------------------------- | :------------------------------------------------- | :--- |
| [appearance](https://www.w3school.com.cn/cssref/pr_appearance.asp) | 允许您将元素设置为标准用户界面元素的外观           | 3    |
| [box-sizing](https://www.w3school.com.cn/cssref/pr_box-sizing.asp) | 允许您以确切的方式定义适应某个区域的具体内容。     | 3    |
| [icon](https://www.w3school.com.cn/cssref/pr_icon.asp)       | 为创作者提供使用图标化等价物来设置元素样式的能力。 | 3    |
| [nav-down](https://www.w3school.com.cn/cssref/pr_nav-down.asp) | 规定在使用 arrow-down 导航键时向何处导航。         | 3    |
| [nav-index](https://www.w3school.com.cn/cssref/pr_nav-index.asp) | 设置元素的 tab 键控制次序。                        | 3    |
| [nav-left](https://www.w3school.com.cn/cssref/pr_nav-left.asp) | 规定在使用 arrow-left 导航键时向何处导航。         | 3    |
| [nav-right](https://www.w3school.com.cn/cssref/pr_nav-right.asp) | 规定在使用 arrow-right 导航键时向何处导航。        | 3    |
| [nav-up](https://www.w3school.com.cn/cssref/pr_nav-up.asp)   | 规定在使用 arrow-up 导航键时向何处导航。           | 3    |
| [outline-offset](https://www.w3school.com.cn/cssref/pr_outline-offset.asp) | 对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓。   | 3    |
| [resize](https://www.w3school.com.cn/cssref/pr_resize.asp)   | 规定是否可由用户对元素的尺寸进行调整。             | 3    |

- resize:是否可由用户调整元素尺寸

```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
border:2px solid;
padding:10px 40px; 
width:300px;
resize:both;
overflow:auto;
}
</style>
</head>
<body>

<div>resize 属性规定是否可由用户调整元素尺寸。</div>

<p><b>注释：</b> Firefox 4+、Safari 以及 Chrome 支持 resize 属性。</p>

</body>
</html>
```
- box-sizing:以确切的方式定义适应某个区域的具体内容
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div.container
{
width:30em;
border:1em solid;
}
div.box
{
box-sizing:border-box;
-moz-box-sizing:border-box; /* Firefox */
-webkit-box-sizing:border-box; /* Safari */
width:50%;
border:1em solid red;
float:left;
}
</style>
</head>
<body>

<div class="container">
<div class="box">这个 div 占据左半部分。</div>
<div class="box">这个 div 占据右半部分。</div>
</div>

</body>
</html>
```
- outline-offset:对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓

```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
margin:20px;
width:150px; 
padding:10px;
height:70px;
border:2px solid black;
outline:2px solid red;
outline-offset:15px;
} 
</style>
</head>
<body>

<p><b>注释：</b>Internet Explorer 和 Opera 不支持 support outline-offset 属性。</p>

<div>这个 div 在边框边缘之外 15 像素处有一个轮廓。</div>

</body>
</html>
```

More info: [CSS3 参考手册](https://www.w3school.com.cn/cssref/index.asp)