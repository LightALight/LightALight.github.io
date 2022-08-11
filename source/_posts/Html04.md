---
title: HTML（四）CSS
date: 2016-08-15 19:23:32
tags: [web,html]
copyright: true
password:
toc: true
---

层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。本文章主要介绍 CSS 的基本概念。

<!--more-->
## Quick Guide

样式定义如何显示 HTML 元素，样式通常存储在样式表中，CSS 指层叠样式表 (Cascading Style Sheets)


样式表允许以多种方式规定样式信息。数字越大，优先展示。

1. 浏览器缺省设置
2. 外部样式表
3. 内部样式表（位于`<head>` 标签内部）
4. 内联样式（在 HTML 元素内部）


### 一、语法

CSS 规则由两个主要的部分构成：

- 选择器
- 一条或多条声明

```css
selector {declaration1; declaration2; ... declarationN }
```
每条声明由一个属性和一个值组成。 

```css
selector {property: value}
```
![](/image/Html04/ct_css_selector.png)


样例：

```html
<!--值的不同写法和单位-->
p { color: #ff0000; }
p { color: #f00; }
p { color: rgb(255,0,0); }
p { color: rgb(100%,0%,0%); }
p {font-family: "sans serif";}
<!--值为若干单词，则要给值加引号-->
p {font-family: "sans serif";}

<!--保持换行和末尾的';' 这样更好修改,避免错误-->
body {
  color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, serif;
  }
```

#### 1.1.继承

```html
<!--通过 CSS 继承，子元素将继承最高级元素（在本例中是 body）所拥有的属性（这些子元素诸如 p, td, ul, ol, ul, li, dl, dt,和 dd）,除了部分浏览器不支持(Netscape 4  IE6 )-->
body  {
     font-family: Verdana, sans-serif;
     }
<!--为了避免遇到不支持,下面做一下子元素设置-->
td, ul, ol, ul, li, dl, dt, dd  {
     font-family: Verdana, sans-serif;
     }
<!--针对p元素设置一个独立的设置-->
p  {
     font-family: Times, "Times New Roman", serif;
     }
```

### 二、创建 CSS

- 外部样式表：使用 `<link>` 标签链接到样式表
```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```
- 内部样式表:使用 `<style>` 标签在文档头部定义内部样式表
```html
<head>
<style type="text/css">
  hr {color: sienna;}
  p {margin-left: 20px;}
  body {background-image: url("images/back40.gif");}
</style>
</head>
```
- 内联样式:相关的标签内使用样式（style）属性

```html
<p style="color: sienna; margin-left: 20px">
This is a paragraph
</p>
```

多重样式：多种样式同时存在，取交集；同样的部分，优先级高覆盖低

### 三、CSS 样式

#### 3.1.背景


| 属性                                                         | 描述                                         |
| :----------------------------------------------------------- | :------------------------------------------- |
| [background](https://www.w3school.com.cn/cssref/pr_background.asp) | 简写属性，作用是将背景属性设置在一个声明中。 |
| [background-attachment](https://www.w3school.com.cn/cssref/pr_background-attachment.asp) | 背景图像是否固定或者随着页面的其余部分滚动。 |
| [background-color](https://www.w3school.com.cn/cssref/pr_background-color.asp) | 设置元素的背景颜色。                         |
| [background-image](https://www.w3school.com.cn/cssref/pr_background-image.asp) | 把图像设置为背景。                           |
| [background-position](https://www.w3school.com.cn/cssref/pr_background-position.asp) | 设置背景图像的起始位置。支持位置关键字、百分比和长度值                    |
| [background-repeat](https://www.w3school.com.cn/cssref/pr_background-repeat.asp) | 设置背景图像是否及如何重复。                 |


```html
<html>
<head>
<style type="text/css">
body {background-color: yellow}
h1 {background-color: #00ff00}
h2 {background-color: transparent}
p {background-color: rgb(250,0,255)}
p.no2 {background-color: gray; padding: 20px;}
</style>
</head>

<body>
<h1>这是标题 1</h1>
<h2>这是标题 2</h2>
<p>这是段落</p>
<p class="no2">这个段落设置了内边距。</p>
</body>
</html>
```

#### 3.2.文本

| 属性                             | 描述                 |
| :---------------------------- | :----------------------- |
| [color](https://www.w3school.com.cn/cssref/pr_text_color.asp) | 设置文本颜色                                                |
| [direction](https://www.w3school.com.cn/cssref/pr_text_direction.asp) | 设置文本方向。                                              |
| [line-height](https://www.w3school.com.cn/cssref/pr_dim_line-height.asp) | 设置行高。                                                  |
| [letter-spacing](https://www.w3school.com.cn/cssref/pr_text_letter-spacing.asp) | 设置字符间距。                                              |
| [text-align](https://www.w3school.com.cn/cssref/pr_text_text-align.asp) | 对齐元素中的文本。                                          |
| [text-decoration](https://www.w3school.com.cn/cssref/pr_text_text-decoration.asp) | 向文本添加修饰。                                            |
| [text-indent](https://www.w3school.com.cn/cssref/pr_text_text-indent.asp) | 缩进元素中文本的首行。                                      |
| text-shadow                                                  | 设置文本阴影。CSS2 包含该属性，但是 CSS2.1 没有保留该属性。 |
| [text-transform](https://www.w3school.com.cn/cssref/pr_text_text-transform.asp) | 控制元素中的字母。                                         |
| unicode-bidi                                                 | 设置文本方向。                                              |
| [white-space](https://www.w3school.com.cn/cssref/pr_text_white-space.asp) | 设置元素中空白的处理方式。                                  |
| [word-spacing](https://www.w3school.com.cn/cssref/pr_text_word-spacing.asp) | 设置字间距。                                                |

```html
<html>
<head>
<style type="text/css">
p {text-indent: 1em}
</style>
</head>

<body>
<p>
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
这是段落中的一些文本。
</p>
</body>
</html>
```

#### 3.3.字体

在 CSS 中，有两种不同类型的字体系列名称：

- 通用字体系列 - 拥有相似外观的字体系统组合（比如 "Serif" 或 "Monospace"）
- 特定字体系列 - 具体的字体系列（比如 "Times" 或 "Courier"）

除了各种特定的字体系列外，CSS 定义了 5 种通用字体系列：

- Serif 字体
- Sans-serif 字体
- Monospace 字体
- Cursive 字体
- Fantasy 字体


| 属性                                | 描述                  |
| :------------------- | :----------------------------------- |
| [font](https://www.w3school.com.cn/cssref/pr_font_font.asp)  | 简写属性。作用是把所有针对字体的属性设置在一个声明中。       |
| [font-family](https://www.w3school.com.cn/cssref/pr_font_font-family.asp) | 设置字体系列。                                               |
| [font-size](https://www.w3school.com.cn/cssref/pr_font_font-size.asp) | 设置字体的尺寸。                                             |
| [font-size-adjust](https://www.w3school.com.cn/cssref/pr_font_font-size-adjust.asp) | 当首选字体不可用时，对替换字体进行智能缩放。（CSS2.1 已删除该属性。） |
| [font-stretch](https://www.w3school.com.cn/cssref/pr_font_font-stretch.asp) | 对字体进行水平拉伸。（CSS2.1 已删除该属性。）                |
| [font-style](https://www.w3school.com.cn/cssref/pr_font_font-style.asp) | 设置字体风格。                                               |
| [font-variant](https://www.w3school.com.cn/cssref/pr_font_font-variant.asp) | 以小型大写字体或者正常字体显示文本。                         |
| [font-weight](https://www.w3school.com.cn/cssref/pr_font_weight.asp) | 设置字体的粗细。                                             |

```html
<html>
<head>
<style type="text/css">
body {font-family:sans-serif;}
p {
    font-family: Times, TimesNR, 'New Century Schoolbook', Georgia, 'New York', serif;
    font-size:1em;
    }
</style>
</head>

<body>
<h1>This is heading 1</h1>
<p style="font-family: Times, TimesNR, 'New Century Schoolbook', Georgia,
 'New York', serif;">This is a paragraph.</p>
<p>This is a paragraph.</p>
<p>This is a paragraph.</p>

<p>...</p>
</body>
</html>
```

#### 3.4.链接

链接的四种状态：

- a:link - 普通的、未被访问的链接
- a:visited - 用户已访问的链接
- a:hover - 鼠标指针位于链接的上方
- a:active - 链接被点击的时刻


```html
<!DOCTYPE html>
<html>
<head>
<style>
a:link {color:#FF0000;}    /* 未被访问的链接 */
a:visited {color:#00FF00;} /* 已被访问的链接 */
a:hover {color:#FF00FF;}   /* 鼠标指针移动到链接上 */
a:active {color:#0000FF;}  /* 正在被点击的链接 */
</style>
</head>

<body>
<p><b><a href="/index.html" target="_blank">这是一个链接</a></b></p>
<p><b>注释：</b>为了使定义生效，a:hover 必须位于 a:link 和 a:visited 之后！！</p>
<p><b>注释：</b>为了使定义生效，a:active 必须位于 a:hover 之后！！</p>
</body>
</html>
```

#### 3.5.列表

| 属性                             | 描述                        |
| :---------------- | :-------------------- |
| [list-style](https://www.w3school.com.cn/cssref/pr_list-style.asp) | 简写属性。用于把所有用于列表的属性设置于一个声明中。 |
| [list-style-image](https://www.w3school.com.cn/cssref/pr_list-style-image.asp) | 将图象设置为列表项标志。                             |
| [list-style-position](https://www.w3school.com.cn/cssref/pr_list-style-position.asp) | 设置列表中列表项标志的位置。                         |
| [list-style-type](https://www.w3school.com.cn/cssref/pr_list-style-type.asp) | 设置列表项标志的类型。                               |
| marker-offset                                                |                                                      |


```html
<html>
<head>
<style type="text/css">
ul.disc {list-style-type: disc}
ul.circle {list-style-type: circle}
ul.square {list-style-type: square}
ul.none {list-style-type: none}
</style>
</head>

<body>
<ul class="disc">
<li>咖啡</li>
<li>茶</li>
<li>可口可乐</li>
</ul>

<ul class="circle">
<li>咖啡</li>
<li>茶</li>
<li>可口可乐</li>
</ul>

<ul class="square">
<li>咖啡</li>
<li>茶</li>
<li>可口可乐</li>
</ul>

<ul class="none">
<li>咖啡</li>
<li>茶</li>
<li>可口可乐</li>
</ul>
</body>

</html>
```

#### 3.6.表格

| 属性                  | 描述                                 |
| :------------------------------ | :-------------- |
| [border-collapse](https://www.w3school.com.cn/cssref/pr_tab_border-collapse.asp) | 设置是否把表格边框合并为单一的边框。 |
| [border-spacing](https://www.w3school.com.cn/cssref/pr_tab_border-spacing.asp) | 设置分隔单元格边框的距离。           |
| [caption-side](https://www.w3school.com.cn/cssref/pr_tab_caption-side.asp) | 设置表格标题的位置。                 |
| [empty-cells](https://www.w3school.com.cn/cssref/pr_tab_empty-cells.asp) | 设置是否显示表格中的空单元格。       |
| [table-layout](https://www.w3school.com.cn/cssref/pr_tab_table-layout.asp) | 设置显示单元、行和列的算法。         |

```html
<html>
<head>
<style type="text/css">
table,td,th
  {
  border:1px solid black;
  }

table
  {
  width:100%;
  }
th
  {
  height:50px;
  }
td
{
height:50px;
vertical-align:bottom;
text-align:right;
padding:15px;
}
</style>
</head>

<body>
<table>
<tr>
<th>Firstname</th>
<th>Lastname</th>
</tr>
<tr>
<td>Bill</td>
<td>Gates</td>
</tr>
<tr>
<td>Steven</td>
<td>Jobs</td>
</tr>
</table>
</body>
</html>
```

#### 3.7.轮廓

| 属性                                                         | 描述                             | CSS  |
| :----------------------------------------------------------- | :------------------------------- | :--- |
| [outline](https://www.w3school.com.cn/cssref/pr_outline.asp) | 在一个声明中设置所有的轮廓属性。 | 2    |
| [outline-color](https://www.w3school.com.cn/cssref/pr_outline-color.asp) | 设置轮廓的颜色。                 | 2    |
| [outline-style](https://www.w3school.com.cn/cssref/pr_outline-style.asp) | 设置轮廓的样式。                 | 2    |
| [outline-width](https://www.w3school.com.cn/cssref/pr_outline-width.asp) | 设置轮廓的宽度。                 | 2    |

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<style type="text/css">
p
{
border: red solid thin;
}
p.dotted {outline-style: dotted}
p.dashed {outline-style: dashed}
p.solid {outline-style: solid}
p.double {outline-style: double}
p.groove {outline-style: groove}
p.ridge {outline-style: ridge}
p.inset {outline-style: inset}
p.outset {outline-style: outset}
</style>
</head>
<body>

<p class="dotted">A dotted outline</p>
<p class="dashed">A dashed outline</p>
<p class="solid">A solid outline</p>
<p class="double">A double outline</p>
<p class="groove">A groove outline</p>
<p class="ridge">A ridge outline</p>
<p class="inset">An inset outline</p>
<p class="outset">An outset outline</p>

<p><b>注释：</b>只有在规定了 !DOCTYPE 时，Internet Explorer 8 （以及更高版本） 才支持 outline-style 属性。</p>
</body>
</html>
```

### 四、框模型

 **CSS 框模型 (Box Model) 规定了元素框处理元素内容、[内边距](#4.1.内边距)、[边框](#4.2.边框) 和 [外边距](#4.3.外边距) 的方式。** 

![](/image/Html04/ct_boxmodel.png)



#### 4.1.内边距

 **元素边框与元素内容之间的空白区域。** 

| 属性                                | 描述             |
| :------------------ | :------------------------------ |
| [padding](https://www.w3school.com.cn/cssref/pr_padding.asp) | 简写属性。作用是在一个声明中设置元素的所内边距属性。 |
| [padding-bottom](https://www.w3school.com.cn/cssref/pr_padding-bottom.asp) | 设置元素的下内边距。                                 |
| [padding-left](https://www.w3school.com.cn/cssref/pr_padding-left.asp) | 设置元素的左内边距。                                 |
| [padding-right](https://www.w3school.com.cn/cssref/pr_padding-right.asp) | 设置元素的右内边距。                                 |
| [padding-top](https://www.w3school.com.cn/cssref/pr_padding-top.asp) | 设置元素的上内边距。                                 |

```html
<html>
<head>
<style type="text/css">
td.test1 {padding: 1.5cm}
td.test2 {padding: 0.5cm 2.5cm}
</style>
</head>

<body>
<table border="1">
<tr>
<td class="test1">
这个表格单元的每个边拥有相等的内边距。
</td>
</tr>
</table>
<br />
<table border="1">
<tr>
<td class="test2">
这个表格单元的上和下内边距是 0.5cm，左和右内边距是 2.5cm。
</td>
</tr>
</table>
</body>

</html>
```

#### 4.2.边框

## CSS 边框属性

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [border](https://www.w3school.com.cn/cssref/pr_border.asp)   | 简写属性，用于把针对四个边的属性设置在一个声明。             |
| [border-style](https://www.w3school.com.cn/cssref/pr_border-style.asp) | 用于设置元素所有边框的样式，或者单独地为各边设置边框样式。   |
| [border-width](https://www.w3school.com.cn/cssref/pr_border-width.asp) | 简写属性，用于为元素的所有边框设置宽度，或者单独地为各边边框设置宽度。 |
| [border-color](https://www.w3school.com.cn/cssref/pr_border-color.asp) | 简写属性，设置元素的所有边框中可见部分的颜色，或为 4 个边分别设置颜色。 |
| [border-bottom](https://www.w3school.com.cn/cssref/pr_border-bottom.asp) | 简写属性，用于把下边框的所有属性设置到一个声明中。           |
| [border-bottom-color](https://www.w3school.com.cn/cssref/pr_border-bottom_color.asp) | 设置元素的下边框的颜色。                                     |
| [border-bottom-style](https://www.w3school.com.cn/cssref/pr_border-bottom_style.asp) | 设置元素的下边框的样式。                                     |
| [border-bottom-width](https://www.w3school.com.cn/cssref/pr_border-bottom_width.asp) | 设置元素的下边框的宽度。                                     |
| [border-left](https://www.w3school.com.cn/cssref/pr_border-left.asp) | 简写属性，用于把左边框的所有属性设置到一个声明中。           |
| [border-left-color](https://www.w3school.com.cn/cssref/pr_border-left_color.asp) | 设置元素的左边框的颜色。                                     |
| [border-left-style](https://www.w3school.com.cn/cssref/pr_border-left_style.asp) | 设置元素的左边框的样式。                                     |
| [border-left-width](https://www.w3school.com.cn/cssref/pr_border-left_width.asp) | 设置元素的左边框的宽度。                                     |
| [border-right](https://www.w3school.com.cn/cssref/pr_border-right.asp) | 简写属性，用于把右边框的所有属性设置到一个声明中。           |
| [border-right-color](https://www.w3school.com.cn/cssref/pr_border-right_color.asp) | 设置元素的右边框的颜色。                                     |
| [border-right-style](https://www.w3school.com.cn/cssref/pr_border-right_style.asp) | 设置元素的右边框的样式。                                     |
| [border-right-width](https://www.w3school.com.cn/cssref/pr_border-right_width.asp) | 设置元素的右边框的宽度。                                     |
| [border-top](https://www.w3school.com.cn/cssref/pr_border-top.asp) | 简写属性，用于把上边框的所有属性设置到一个声明中。           |
| [border-top-color](https://www.w3school.com.cn/cssref/pr_border-top_color.asp) | 设置元素的上边框的颜色。                                     |
| [border-top-style](https://www.w3school.com.cn/cssref/pr_border-top_style.asp) | 设置元素的上边框的样式。                                     |
| [border-top-width](https://www.w3school.com.cn/cssref/pr_border-top_width.asp) | 设置元素的上边框的宽度。                                     |

```html
<html>
<head>
<style type="text/css">
p 
{
border-style:solid;
border-left:thick double #ff0000;
}
</style>
</head>

<body>
<p>This is some text in a paragraph.</p>
</body>
</html>
```

#### 4.3.外边距

 **围绕在元素边框的空白区域是外边距。** 



| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [margin](https://www.w3school.com.cn/cssref/pr_margin.asp)   | 简写属性。在一个声明中设置所有外边距属性。margin: top right bottom left |
| [margin-bottom](https://www.w3school.com.cn/cssref/pr_margin-bottom.asp) | 设置元素的下外边距。                                         |
| [margin-left](https://www.w3school.com.cn/cssref/pr_margin-left.asp) | 设置元素的左外边距。                                         |
| [margin-right](https://www.w3school.com.cn/cssref/pr_margin-right.asp) | 设置元素的右外边距。                                         |
| [margin-top](https://www.w3school.com.cn/cssref/pr_margin-top.asp) | 设置元素的上外边距。                                         |

外边距少于 4 个值。规则如下：

- 如果缺少左外边距的值，则使用右外边距的值。
- 如果缺少下外边距的值，则使用上外边距的值。
- 如果缺少右外边距的值，则使用上外边距的值。

```html
<html>
<head>
<style type="text/css">
p.margin {margin: 2cm}
</style>
</head>

<body>

<p>这个段落没有指定外边距。</p>

<p class="margin">这个段落带有指定的外边距。这个段落带有指定的外边距。这个段落带有指定的外边距。这个段落带有指定的外边距。这个段落带有指定的外边距。</p>

<p>这个段落没有指定外边距。</p>

</body>

</html>

```

**当两个垂直外边距相遇时，它们将形成一个外边距。**  **合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。** 

![](/image/Html04/ct_css_margin_collapsing_example_1.png)
![](/image/Html04/ct_css_margin_collapsing_example_2.png)
![](/image/Html04/ct_css_margin_collapsing_example_3.png)
![](/image/Html04/ct_css_margin_collapsing_example_4.png)

### 五、定位

定位属性允许你对元素进行定位。 

- [普通流](#5.1.相对定位)： 普通流中的元素的位置由元素在 (X)HTML 中的位置决定。 
- [绝对定位](#5.2.绝对定位)
- [浮动](#5.3.浮动)

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [position](https://www.w3school.com.cn/cssref/pr_class_position.asp) | 把元素放置到一个静态的、相对的、绝对的、或固定的位置中。     |
| [top](https://www.w3school.com.cn/cssref/pr_pos_top.asp)     | 定义了一个定位元素的上外边距边界与其包含块上边界之间的偏移。 |
| [right](https://www.w3school.com.cn/cssref/pr_pos_right.asp) | 定义了定位元素右外边距边界与其包含块右边界之间的偏移。       |
| [bottom](https://www.w3school.com.cn/cssref/pr_pos_bottom.asp) | 定义了定位元素下外边距边界与其包含块下边界之间的偏移。       |
| [left](https://www.w3school.com.cn/cssref/pr_pos_left.asp)   | 定义了定位元素左外边距边界与其包含块左边界之间的偏移。       |
| [overflow](https://www.w3school.com.cn/cssref/pr_pos_overflow.asp) | 设置当元素的内容溢出其区域时发生的事情。                     |
| [clip](https://www.w3school.com.cn/cssref/pr_pos_clip.asp)   | 设置元素的形状。元素被剪入这个形状之中，然后显示出来。       |
| [vertical-align](https://www.w3school.com.cn/cssref/pr_pos_vertical-align.asp) | 设置元素的垂直对齐方式。                                     |
| [z-index](https://www.w3school.com.cn/cssref/pr_pos_z-index.asp) | 设置元素的堆叠顺序。                                         |

#### 5.1.相对定位

 相对定位实际上被看作普通流定位模型的一部分，因为元素的位置相对于它在普通流中的位置。 

```html
<html>
<head>
<style type="text/css">
h2.pos_left
{
position:relative;
left:-20px
}
h2.pos_right
{
position:relative;
left:20px
}
</style>
</head>

<body>
<h2>这是位于正常位置的标题</h2>
<h2 class="pos_left">这个标题相对于其正常位置向左移动</h2>
<h2 class="pos_right">这个标题相对于其正常位置向右移动</h2>
<p>相对定位会按照元素的原始位置对该元素进行移动。</p>
<p>样式 "left:-20px" 从元素的原始左侧位置减去 20 像素。</p>
<p>样式 "left:20px" 向元素的原始左侧位置增加 20 像素。</p>
</body>

</html>
```

#### 5.2.绝对定位

 绝对定位使元素的位置与文档流无关，  普通流中其它元素的布局就像绝对定位的元素不存在一样 。

```html
<html>
<head>
<style type="text/css">
h2.pos_abs
{
position:absolute;
left:100px;
top:150px
}
</style>
</head>

<body>
<h2 class="pos_abs">这是带有绝对定位的标题</h2>
<p>通过绝对定位，元素可以放置到页面上的任何位置。下面的标题距离页面左侧 100px，距离页面顶部 150px。</p>
</body>

</html>
```



#### 5.3.浮动

**浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。**

**由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样。**

- **float** ：元素的浮动。
- **clear**：元素的哪一侧不允许其他浮动元素

![](/image/Html04/ct_css_positioning_floating_right_example.png)

```html
<html>
<head>
<style type="text/css">
img 
{
float:right
}
</style>
</head>

<body>
<p>在下面的段落中，我们添加了一个样式为 <b>float:right</b> 的图像。结果是这个图像会浮动到段落的右侧。</p>
<p>
<img src="/i/eg_cute.gif" />
This is some text. This is some text. This is some text.
This is some text. This is some text. This is some text.
This is some text. This is some text. This is some text.
This is some text. This is some text. This is some text.
</p>
</body>

</html>
```
```html
<html>

<head>
<style type="text/css">
img
  {
  float:left;
  clear:both;
  }
</style>
</head>

<body>
<img src="/i/eg_smile.gif" />
<img src="/i/eg_smile.gif" />
</body>
</html>
```

### 六、选择器

#### 6.1.元素选择器

元素选择器又称为类型选择器（type selector）。

```html
<html>
<head>
<style type="text/css">
html {color:black;}
p {color:blue;}
h2 {color:silver;}
</style>
</head>

<body>
<h1>这是 heading 1</h1>
<h2>这是 heading 2</h2>
<p>这是一段普通的段落。</p>
</body>
</html>
```

#### 6.2.选择器的分组
```html
h1,h2,h3,h4,h5,h6 {
  color: green;
  }
* {color:red;}
```

#### 6.3.派生选择器

根据文档的上下文关系来确定某个标签的样式。

```html
li strong {
    font-style: italic;
    font-weight: normal;
  }

<p><strong>我是粗体字，不是斜体字，因为我不在列表当中，所以这个规则对我不起作用</strong></p>

<ol>
<li><strong>我是斜体字。这是因为 strong 元素位于 li 元素内。</strong></li>
<li>我是正常的字体。</li>
</ol>
```

#### 6.4.类选择器

在 CSS 中，类选择器以一个点号显示：
```html
.center {text-align: center}

<h1 class="center">
This heading will be center-aligned
</h1>

<p class="center">
This paragraph will also be center-aligned.
</p>

<!-- 与派生器结合-->
.fancy td {
	color: #f60;
	background: #666;
	}

td.fancy {
	color: #f60;
	background: #666;
	}
```

```html
<html>
<head>
<!-- 多类选择器:通过把两个类选择器链接在一起，选择同时包含这些类名的元素 -->
<style type="text/css">
.important {font-weight:bold;}
.warning {font-style:italic;}
.important.warning {background:silver;}
</style>
</head>

<body>
<p class="important">This paragraph is very important.</p>

<p class="warning">This is a warning.</p>

<p class="important urgent warning">This paragraph is a very important warning.</p>

<p>This is a paragraph.</p>

<p>...</p>
</body>
</html>
```

#### 6.5.id 选择器

为标有特定 id 的 HTML 元素指定特定的样式。以 "#" 来定义。

```html
#red {color:red;}
#green {color:green;}

<p id="red">这个段落是红色。</p>
<p id="green">这个段落是绿色。</p>

<!-- 与派生器结合-->
#sidebar p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}
```
注意事项:
- 只能在文档中使用一次
- 不能使用 ID 词列表
- 区分大小写

#### 6.6.属性选择器

为拥有指定属性的 HTML 元素设置样式，而不仅限于 class 和 id 属性。
只有在规定了 !DOCTYPE 时，IE7 和 IE8 才支持属性选择器。在 IE6 及更低的版本中，不支持属性选择。


| 选择器                  | 描述                                     |
| :-------------------------------- | :------------------------------------- |
| [[*attribute*\]](https://www.w3school.com.cn/cssref/selector_attribute.asp) | 用于选取带有指定属性的元素。                                 |
| [[*attribute*=*value*\]](https://www.w3school.com.cn/cssref/selector_attribute_value.asp) | 用于选取带有指定属性和值的元素。属性与属性值必须完全匹配                 |
| [[*attribute*~=*value*\]](https://www.w3school.com.cn/cssref/selector_attribute_value_contain.asp) | 用于选取属性值中包含指定词汇的元素。                         |
| [[*attribute*\|=*value*\]](https://www.w3school.com.cn/cssref/selector_attribute_value_start.asp) | 用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。 |
| [[*attribute*^=*value*\]](https://www.w3school.com.cn/cssref/selector_attr_begin.asp) | 匹配属性值以指定值开头的每个元素。                           |
| [[*attribute*$=*value*\]](https://www.w3school.com.cn/cssref/selector_attr_end.asp) | 匹配属性值以指定值结尾的每个元素。                           |
| [[*attribute**=*value*\]](https://www.w3school.com.cn/cssref/selector_attr_contain.asp) | 匹配属性值中包含指定值的每个元素。                           |

```html
*[title] {color:red;}
a[href][title] {color:red;}
[title=W3School]
{
border:5px solid blue;
}
```

#### 6.7.后代选择器

 在后代选择器中，规则左边的选择器一端包括两个或多个用空格分隔的选择器。选择器之间的空格是一种结合符（combinator）。每个空格结合符可以解释为“... 在 ... 找到”、“... 作为 ... 的一部分”、“... 作为 ... 的后代”，但是要求必须从右向左读选择器。 

```html
<html>
<head>
<style type="text/css">
ul em {color:red; font-weight:bold;}
</style>
</head>

<body>
<ul>
  <li>List item 1
    <ol>
      <li>List item 1-1</li>
      <li>List item 1-2</li>
      <li>List item 1-3
        <ol>
          <li>List item 1-3-1</li>
          <li>List item <em>1-3-2</em></li>
          <li>List item 1-3-3</li>
        </ol>
      </li>
      <li>List item 1-4</li>
    </ol>
  </li>
  <li>List item 2</li>
  <li>List item 3</li>
</ul>
</body>
</html>
```

#### 6.8.子元素选择器

 **选择作为某元素子元素的元素，子选择器使用了大于号（子结合符）。 **

```html
<!DOCTYPE HTML>
<html>
<head>
<!--选择只作为 h1 元素子元素的 strong 元素 -->
<style type="text/css">
h1 > strong {color:red;}
</style>
</head>

<body>
<h1>This is <strong>very</strong> <strong>very</strong> important.</h1>
<h1>This is <em>really <strong>very</strong></em> important.</h1>
</body>
</html>
```

#### 6.9.相邻兄弟选择器

 **选择紧接在另一元素后的元素，且二者有相同父元素。**  相邻兄弟选择器使用了加号（+），即相邻兄弟结合符（Adjacent sibling combinator）。 

```html
<div>
  <ul>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
  </ul>
  <ol>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
  </ol>
</div>
```

#### 6.10.伪类 (Pseudo-classes)

 **用于向某些选择器添加特殊的效果。** 

```html
selector : pseudo-class {property: value}
selector.class : pseudo-class {property: value}
```
*W3C*："W3C" 列指示出该属性在哪个 CSS 版本中定义（CSS1 还是 CSS2）。

| 属性                                                         | 描述                                     | CSS  |
| :----------------------------------------------------------- | :--------------------------------------- | :--- |
| [:active](https://www.w3school.com.cn/cssref/pr_pseudo_active.asp) | 向被激活的元素添加样式。                 | 1    |
| [:focus](https://www.w3school.com.cn/cssref/pr_pseudo_focus.asp) | 向拥有键盘输入焦点的元素添加样式。       | 2    |
| [:hover](https://www.w3school.com.cn/cssref/pr_pseudo_hover.asp) | 当鼠标悬浮在元素上方时，向元素添加样式。 | 1    |
| [:link](https://www.w3school.com.cn/cssref/pr_pseudo_link.asp) | 向未被访问的链接添加样式。               | 1    |
| [:visited](https://www.w3school.com.cn/cssref/pr_pseudo_visited.asp) | 向已被访问的链接添加样式。               | 1    |
| [:first-child](https://www.w3school.com.cn/cssref/pr_pseudo_first-child.asp) | 向元素的第一个子元素添加样式。           | 2    |
| [:lang](https://www.w3school.com.cn/cssref/pr_pseudo_lang.asp) | 向带有指定 lang 属性的元素添加样式。     | 2    |

```html
<html>
<head>

<style type="text/css">
a:link {color: #FF0000}
a:visited {color: #00FF00}
a:hover {color: #FF00FF}
a:active {color: #0000FF}
</style>

</head>

<body>

<p><b><a href="/index.html" target="_blank">这是一个链接。</a></b></p>
<p><b>注释：</b>在 CSS 定义中，a:hover 必须位于 a:link 和 a:visited 之后，这样才能生效！</p>
<p><b>注释：</b>在 CSS 定义中，a:active 必须位于 a:hover 之后，这样才能生效！</p>

</body>
</html>
```

**注： 伪类名称对大小写不敏感。 **

####  6.11.伪元素 (Pseudo-elements)

用于向某些选择器设置特殊效果。

```html
selector:pseudo-element {property:value;}
selector.class:pseudo-element {property:value;}
```

*W3C*："W3C" 列指示出该属性在哪个 CSS 版本中定义（CSS1 还是 CSS2）。

| 属性                                                         | 描述                             | CSS  |
| :----------------------------------------------------------- | :------------------------------- | :--- |
| [:first-letter](https://www.w3school.com.cn/cssref/pr_pseudo_first-letter.asp) | 向文本的第一个字母添加特殊样式。 | 1    |
| [:first-line](https://www.w3school.com.cn/cssref/pr_pseudo_first-line.asp) | 向文本的首行添加特殊样式。       | 1    |
| [:before](https://www.w3school.com.cn/cssref/pr_pseudo_before.asp) | 在元素之前添加内容。             | 2    |
| [:after](https://www.w3school.com.cn/cssref/pr_pseudo_after.asp) | 在元素之后添加内容。             |      |

```html
<html>

<head>
<style type="text/css">
p:first-letter
  {
  color:#ff0000;
  font-size:xx-large;
  }

p:first-line 
  {
  color:#0000ff;
  font-variant:small-caps;
  }
</style>
</head>

<body>
<p>You can combine the :first-letter and :first-line pseudo-elements to add a special effect to the first letter and the first line of a text!</p>
</body>

</html>
```

### 七、高级

#### 7.1.对齐
使用多种属性来水平对齐元素。

- 对齐块元素
```html
<h1>
<p>
<div>
```
- margin 属性来水平对齐
```html
<!DOCTYPE html>
<html>
<head>
<style>
.center
{
margin:auto;
width:70%;
background-color:#b0e0e6;
}
</style>
</head>

<body>

<div class="center">
<p>这是一个段落。这是一个段落。这是一个段落。这是一个段落。这是一个段落。</p>
<p>这是一个段落。这是一个段落。这是一个段落。这是一个段落。这是一个段落。</p>
</div>

<p><b>注释：</b>除非已经声明了 !DOCTYPE，否则使用 margin:auto 在 IE8 以及更早的版本中是无效的。</p>
</body>
</html>
```
- position 属性进行左和右对齐
```html
<!DOCTYPE html>
<html>
<head>
<style>
body
{
margin:0;
padding:0;
}
.container
{
position:relative;
width:100%;
}
.right
{
position:absolute;
right:0px;
width:300px;
background-color:#b0e0e6;
}
</style>
</head>

<body>
<div class="container">
<div class="right">
<p><b>注释：</b>当使用 position 属性进行对齐时，请始终包含 !DOCTYPE 声明！如果省略，则会在 IE 浏览器中产生奇怪的结果。</p>
</div>
</div>

</body>
</html>
```
- float 属性来进行左和右对齐
```html
<!DOCTYPE html>
<html>
<head>
<style>
body
{
margin:0;
padding:0;
}
.right
{
float:right;
width:300px;
background-color:#b0e0e6;
}
</style>
</head>

<body>

<div class="right">
<p><b>注释：</b>当使用 float 属性进行对齐时，请始终包含 !DOCTYPE 声明！如果省略，则会在 IE 浏览器中产生奇怪的结果。</p>
</div>

</body>
</html>
```
#### 7.2.尺寸

| 属性                                                         | 描述                 |
| :----------------------------------------------------------- | :------------------- |
| [height](https://www.w3school.com.cn/cssref/pr_dim_height.asp) | 设置元素的高度。     |
| [line-height](https://www.w3school.com.cn/cssref/pr_dim_line-height.asp) | 设置行高。           |
| [max-height](https://www.w3school.com.cn/cssref/pr_dim_max-height.asp) | 设置元素的最大高度。 |
| [max-width](https://www.w3school.com.cn/cssref/pr_dim_max-width.asp) | 设置元素的最大宽度。 |
| [min-height](https://www.w3school.com.cn/cssref/pr_dim_min-height.asp) | 设置元素的最小高度。 |
| [min-width](https://www.w3school.com.cn/cssref/pr_dim_min-width.asp) | 设置元素的最小宽度。 |
| [width](https://www.w3school.com.cn/cssref/pr_dim_width.asp) | 设置元素的宽度。     |

#### 7.3 分类

| 属性                                                         | 描述                                                     |
| :----------------------------------------------------------- | :------------------------------------------------------- |
| [clear](https://www.w3school.com.cn/cssref/pr_class_clear.asp) | 设置一个元素的侧面是否允许其他的浮动元素。               |
| [cursor](https://www.w3school.com.cn/cssref/pr_class_cursor.asp) | 规定当指向某元素之上时显示的指针类型。                   |
| [display](https://www.w3school.com.cn/cssref/pr_class_display.asp) | 设置是否及如何显示元素。                                 |
| [float](https://www.w3school.com.cn/cssref/pr_class_float.asp) | 定义元素在哪个方向浮动。                                 |
| [position](https://www.w3school.com.cn/cssref/pr_class_position.asp) | 把元素放置到一个静态的、相对的、绝对的、或固定的位置中。 |
| [visibility](https://www.w3school.com.cn/cssref/pr_class_visibility.asp) | 设置元素是否可见或不可见。                               |

#### 7.4.导航条

- 链接列表

```html
<!DOCTYPE html>
<html>
<body>
<ul>
<li><a href="#home">Home</a></li>
<li><a href="#news">News</a></li>
<li><a href="#contact">Contact</a></li>
<li><a href="#about">About</a></li>
</ul>

<p><b>注释：</b>我们使用在测试链接中使用了 href="#"。在真实的网站中，应该是真实的 URL。</p>

</body>
</html>
```

- 垂直导航栏

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <style>
  ul
  {
  list-style-type:none;
  margin:0;
  padding:0;
  }
  a
  {
  display:block;
  width:60px;
  background-color:#dddddd;
  }
  </style>
  </head>
  
  <body>
  <ul>
  <li><a href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li><a href="#contact">Contact</a></li>
  <li><a href="#about">About</a></li>
  </ul>
  
  <p>为了显示出链接区域，我们为链接添加了背景色。</p>
  <p>请注意，全部链接区域都是可点击的，不仅仅是文本。</p>
  </body>
  </html>
  ```

  

- 水平导航栏

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <style>
  ul
  {
  list-style-type:none;
  margin:0;
  padding:0;
  }
  li
  {
  display:inline;
  }
  </style>
  </head>
  
  <body>
  <ul>
  <li><a href="#home">Home</a></li>
  <li><a href="#news">News</a></li>
  <li><a href="#contact">Contact</a></li>
  <li><a href="#about">About</a></li>
  </ul>
  
  </body>
  </html>
  ```
- 对列表项进行浮动

```html
<!DOCTYPE html>
<html>
<head>
<style>
ul
{
list-style-type:none;
margin:0;
padding:0;
overflow:hidden;
}
li
{
float:left;
}
a
{
display:block;
width:60px;
background-color:#dddddd;
}
</style>
</head>

<body>
<ul>
<li><a href="#home">Home</a></li>
<li><a href="#news">News</a></li>
<li><a href="#contact">Contact</a></li>
<li><a href="#about">About</a></li>
</ul>

<p><b>注释：</b>如果没有规定 !DOCTYPE，则浮动项目会产生意想不到的结果。</p>

<p>为了显示出链接区域，我们为链接添加了背景色。</p>

<p><b>注释：</b>向 ul 元素添加 overflow:hidden，是为了防止 li 元素出现在列表之外。</p>

</body>
</html>
```

#### 7.5.图片库

```html
<!doctype html>
<html>
<head>
<style>
div.img
  {
  margin:3px;
  border:1px solid #bebebe;
  height:auto;
  width:auto;
  float:left;
  text-align:center;
  }
div.img img
  {
  display:inline;
  margin:3px;
  border:1px solid #bebebe;
  }
div.img a:hover img
  {
  border:1px solid #333333;
  }
div.desc
  {
  text-align:center;
  font-weight:normal;
  width:150px;
  font-size:12px;
  margin:10px 5px 10px 5px;
  }
</style>
</head>
<body>

<div class="img">
  <a target="_blank" href="/i/tulip_ballade.jpg">
  <img src="/i/tulip_ballade_s.jpg" alt="Ballade" width="160" height="160">
  </a>
  <div class="desc">在此处添加对图像的描述</div>
</div>

<div class="img">
  <a target="_blank" href="/i/tulip_flaming_club.jpg">
  <img src="/i/tulip_flaming_club_s.jpg" alt="Ballade" width="160" height="160">
  </a>
  <div class="desc">在此处添加对图像的描述</div>
</div>

<div class="img">
  <a target="_blank" href="/i/tulip_fringed_family.jpg">
  <img src="/i/tulip_fringed_family_s.jpg" alt="Ballade" width="160" height="160">
  </a>
  <div class="desc">在此处添加对图像的描述</div>
</div>

<div class="img">
  <a target="_blank" href="/i/tulip_peach_blossom.jpg">
  <img src="/i/tulip_peach_blossom_s.jpg" alt="Ballade" width="160" height="160">
  </a>
  <div class="desc">在此处添加对图像的描述</div>
</div>

</body>
</html>
```

#### 7.6.透明

- 图片透明

  ```html
  img
  {
  opacity:0.4;
  filter:alpha(opacity=40); /* 针对 IE8 以及更早的版本 */
  }
  ```

- 图片透明，当指针在上面不透明

  ```html
  img
  {
  opacity:0.4;
  filter:alpha(opacity=40); /* 针对 IE8 以及更早的版本 */
  }
  img:hover
  {
  opacity:1.0;
  filter:alpha(opacity=100); /* 针对 IE8 以及更早的版本 */
  }
  ```

- 透明框中的文本

```html
<!DOCTYPE html>
<html>
<head>
<style>
div.background
{
  width: 400px;
  height: 266px;
  background: url('/i/tulip_peach_blossom_w.jpg') no-repeat;
  border: 1px solid black;
}

div.transbox
{
  width: 338px;
  height: 204px;
  margin:30px;
  background-color: #ffffff;
  border: 1px solid black;
  /* for IE */
  filter:alpha(opacity=60);
  /* CSS3 standard */
  opacity:0.6;
}

div.transbox p
{
  margin: 30px 40px;
}
</style>
</head>

<body>

<div class="background">
<div class="transbox">
<p>
This is some text that is placed in the transparent box.
This is some text that is placed in the transparent box.
This is some text that is placed in the transparent box.
This is some text that is placed in the transparent box.
This is some text that is placed in the transparent box.
</p>
</div>
</div>

</body>
</html>
```

#### 7.7.媒介类型

 **允许你定义以何种媒介来提交文档。文档可以被显示在显示器、纸媒介或者听觉浏览器等等。** 

**注释：**媒介类型名称对大小写不敏感。

| 媒介类型   | 描述                                                   |
| :--------- | :----------------------------------------------------- |
| all        | 用于所有的媒介设备。                                   |
| aural      | 用于语音和音频合成器。                                 |
| braille    | 用于盲人用点字法触觉回馈设备。                         |
| embossed   | 用于分页的盲人用点字法打印机。                         |
| handheld   | 用于小的手持的设备。                                   |
| print      | 用于打印机。                                           |
| projection | 用于方案展示，比如幻灯片。                             |
| screen     | 用于电脑显示器。                                       |
| tty        | 用于使用固定密度字母栅格的媒介，比如电传打字机和终端。 |
| tv         | 用于电视机类型的设备。                                 |

```html
<html>
<head>
<!--浏览器在显示器上显示 14 像素的 Verdana 字体。但是假如页面需要被打印，将使用 10 个像素的 Times 字体。注意：font-weight 被设置为粗体，不论显示器还是纸媒介-->
<style>
@media screen
{
p.test {font-family:verdana,sans-serif; font-size:14px}
}

@media print
{
p.test {font-family:times,serif; font-size:10px}
}

@media screen,print
{
p.test {font-weight:bold}
}
</style>

</head>

<body>....</body>

</html>
```

### 八、注意事项

- 避免使用Internet Explorer Behaviors：只有 Internet Explorer 支持 behavior 属性。

More info: [CSS 参考手册](https://www.w3school.com.cn/cssref/index.asp)