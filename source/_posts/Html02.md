---
title: HTML（二）XHTML
date: 2016-06-15 19:23:32
tags: [web,html]
copyright: true
password:
toc: true
---

**XHTML 是以 XML 格式编写的 HTML。** 
XHTML 于2000年的1月26日成为 W3C 标准，W3C 将 XHTML 定义为最新的HTML版本。XHTML 将逐渐取代 HTML。本文章主要介绍 XHTML 的基本概念。

<!--more-->
## Quick Guide


### 一、为什么要使用XHTML

万维网上的许多页面都包含着糟糕的 HTML 代码，市场中存在着不同的浏览器技术，某些浏览器没有能力和手段来解释糟糕的标记语言。
XML 是一种必须正确标记且格式良好的标记语言。通过结合 XML 和 HTML 的长处，开发出了 XHTML。

### 二、文档结构

- XHTML DOCTYPE 是*强制性的*
- `<html>` 中的 XML namespace 属性是*强制性的*
- `<html>`、`<head>`、`<title>` 以及 `<body>` 也是*强制性的*

一个 XHTML 文档有三个主要的部分：

- DOCTYPE:文档类型声明, DTD 规定了使用通用标记语言(SGML)的网页的语法 
  - STRICT（严格类型）: 需要干净的标记，避免表现上的混乱。请与层叠样式表配合使用。 
  - TRANSITIONAL（过渡类型）: 当需要利用 HTML 在表现上的特性时，并且当需要为那些不支持层叠样式表的浏览器编写 XHTML 时。 
  - FRAMESET（框架类型）: 需要使用HTML框架将浏览器窗口分割为两部分或更多框架时。 
- Head
- Body

```html
<!-- 文档类型声明定义文档的类型 -->
<!DOCTYPE html
PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html>
<head>
<title>simple document</title>
</head>
<body>
<p>a simple paragraph</p>
</body>
</html>
```

  


### 三、语法

#### 元素语法

- XHTML 元素必须*正确嵌套*
- XHTML 元素必须始终*关闭*
- XHTML 元素必须*小写*
- XHTML 文档必须有*一个根元素*
- XHTML DTD 定义了强制使用的 HTML 元素

#### 属性语法

- XHTML 属性必须使用*小写*
- XHTML 属性值必须用*引号包围*
- XHTML 属性最小化也是*禁止的*
- 用 Id 属性代替 name 属性


### 四、HTML升级至 XHTML

1. 向每张页面的第一行添加 XHTML <!DOCTYPE>
2. 向每张页面的 html 元素添加 xmlns 属性
3. 把所有元素名改为小写
4. 关闭所有空元素：`<hr>` 和 `<br>` 标签应该被替换为 `<hr />` 和 `<br />`
5. 把所有属性名改为小写
6. 为所有属性值加引号
7. 验证站点:
   1. 通过 DTD 验证 XHTML
   2. 使用 W3C 验证器：http://validator.w3.org/check?uri=https://www.baidu.com （uri=被验证网页）

### 五、模块

XHTML 是简单而庞大的语言。XHTML 包含了网站开发者需要的大多数功能。对于某些特殊的用途，XHTML 太大且太复杂，而对于其他的用途，它又太简单了。

通过将 XHTML 分为若干模块，W3C 已经创造出数套小巧且定义良好的 XHTML 元素，这些元素既可被独立应用于简易设备，又可以与其他 XML 标准并入大型且更复杂的应用程序。

通过使用模块化的 XHTML，产品和软件设计者可以：

- 选择被某种设备所支持的元素。
- 在不打破 XHTML 标准的情况下，使用 XML 对 XHTML 进行扩展。
- 针对小型设备，对 XHTML 进行简化。
- 通过添加新的 XML 功能（比如 MathML, SVG, 语音和多媒体），针对复杂的应用对 XHTML 进行扩展。
- 定义 XHTML 框架，比如 XHTML BASIC （针对移动设备的 XHTML 子集）。

W3C 已将 XHTML 的定义分为28种模型：

| 模块名称        | 描述                                   |
| :------------------- | :----------------------------------- |
| Applet Module (Applet模块)                    | 定义已被废弃的applet元素。                      |
| Base Module (基础模块)                        | 定义基本元素。                                  |
| Basic Forms Module (基础表单模块)             | 定义基本的表单元素 (forms)。                    |
| Basic Tables Module (基础表格模块)            | 定义基本的表格元素 (table)。                    |
| Bi-directional Text Module (双向文本模块)     | 定义bdo元素。                                   |
| Client Image Map Module(客户端图像映射模块)   | 定义浏览器端图像映射元素(image map elements)。  |
| Edit Module (编辑模块)                        | 定义编辑元素删除和插入。                        |
| Forms Module (表单模块)                       | 定义所有在表单中使用的元素。                    |
| Frames Module (框架模块)                      | 定义frameset元素。                              |
| Hypertext Module (超文本模块)                 | 定义a元素。                                     |
| Iframe Module (内联框架模块)                  | 定义iframe元素。                                |
| Image Module (图像模块)                       | 定义图像元素 (img)。                            |
| Intrinsic Events Module ()                    | 定义事件属性 (event)，比如onblur和onchange。    |
| Legacy Module (遗留模块)                      | 定义被废弃的元素和属性。                        |
| Link Module (链接模块)                        | 定义链接 (link)元素。                           |
| List Module (列表模块)                        | 定义列表元素ol, li, ul, dd, dt,和dl。           |
| Metainformation Module (元信息模块)           | 定义meta元素。                                  |
| Name Identification Module (名称识别模块)     | 定义已被废弃的name属性。                        |
| Object Module (对象模块)                      | 定义对象元素 (object)和param元素。              |
| Presentation Module (表现模块)                | 定义表现元素比如b和i。                          |
| Scripting Module (脚本模块)                   | 定义脚本 (script)和无脚本 (noscript)元素。      |
| Server Image Map Module(服务器端图像映射模块) | 定义服务器端图像映射(server side image map)元素 |
| Structure Module (结构模块)                   | 定义以下元素：html, head, title and body。      |
| Style Attribute Module (样式属性模块)         | 定义样式属性。                                  |
| Style Sheet Module (样式表模块)               | 定义样式元素。                                  |
| Tables Module (表格模块)                      | 定义用于表格中的元素。                          |
| Target Module (Target模块)                    | 定义target属性。                                |
| Text Module (文本模块)                        | 定义文本容器元素 (text container)，比如p和h1。  |

### 六、标准属性

#### 核心属性 
以下标签不提供下面的属性：base, head, html, meta, param, script, style, 以及 title 元素。

| 属性  | 值                       | 描述                   |
| :---- | :----------------------- | :--------------------- |
| class | class_rule 或 style_rule | 元素的类(class)        |
| id    | id_name                  | 元素的某个特定id       |
| style | 样式定义                 | 内联样式定义           |
| title | 提示文本                 | 显示于提示工具中的文本 |

#### 语言属性 (Language Attributes)

以下标签不提供下面的属性：base, br, frame, frameset, hr, iframe, param, 以及 script 元素。

| 属性 | 值         | 描述           |
| :--- | :--------- | :------------- |
| dir  | ltr \| rtl | 设置文本的方向 |
| lang | 语言代码   | 设置语言代码   |

#### 键盘属性 (Keyboard Attributes)

| 属性      | 值   | 描述                       |
| :-------- | :--- | :------------------------- |
| accesskey | 字符 | 设置访问某元素的键盘快捷键 |
| tabindex  | 数   | 设置某元素的Tab次序        |


### 七、事件
在现代浏览器中都内置有大量的事件处理器。这些处理器会监视特定的条件或用户行为，例如鼠标单击或浏览器窗口中完成加载某个图像。通过使用客户端的 JavaScript，可以将某些特定的事件处理器作为属性添加给特定的标签，并可以在事件发生时执行一个或多个 JavaScript 命令或函数。

事件处理器的值是一个或一系列以分号隔开的 Javascript 表达式、方法和函数调用，并用引号引起来。当事件发生时，浏览器会执行这些代码。例如，当您把鼠标移动到一个超链接时，会启动一个 JavaScript 函数。支持 JavaScript 的浏览器支持 <a> 标签中的一个特殊的 "mouse over"事件处理器 - 被称为 onmouseover 来完成这项工作：

```html
<a href="/index.html" onmouseover="alert('Welcome');return false"></a>
```

#### 窗口事件 (Window Events)

仅在 body 和 frameset 元素中有效。

| 属性     | 值   | 描述                   |
| :------- | :--- | :--------------------- |
| onload   | 脚本 | 当文档被载入时执行脚本 |
| onunload | 脚本 | 当文档被卸下时执行脚本 |

#### 表单元素事件 (Form Element Events)

仅在表单元素中有效。

| 属性     | 值   | 描述                     |
| :------- | :--- | :----------------------- |
| onchange | 脚本 | 当元素改变时执行脚本     |
| onsubmit | 脚本 | 当表单被提交时执行脚本   |
| onreset  | 脚本 | 当表单被重置时执行脚本   |
| onselect | 脚本 | 当元素被选取时执行脚本   |
| onblur   | 脚本 | 当元素失去焦点时执行脚本 |
| onfocus  | 脚本 | 当元素获得焦点时执行脚本 |

#### 键盘事件 (Keyboard Events)

在下列元素中无效：base, bdo, br, frame, frameset, head, html, iframe, meta, param, script, style, 以及 title 元素。

| 属性       | 值   | 描述                           |
| :--------- | :--- | :----------------------------- |
| onkeydown  | 脚本 | 当键盘被按下时执行脚本         |
| onkeypress | 脚本 | 当键盘被按下后又松开时执行脚本 |
| onkeyup    | 脚本 | 当键盘被松开时执行脚本         |

#### 鼠标事件 (Mouse Events)

在下列元素中无效：base, bdo, br, frame, frameset, head, html, iframe, meta, param, script, style, title 元素。

| 属性        | 值   | 描述                                 |
| :---------- | :--- | :----------------------------------- |
| onclick     | 脚本 | 当鼠标被单击时执行脚本               |
| ondblclick  | 脚本 | 当鼠标被双击时执行脚本               |
| onmousedown | 脚本 | 当鼠标按钮被按下时执行脚本           |
| onmousemove | 脚本 | 当鼠标指针移动时执行脚本             |
| onmouseout  | 脚本 | 当鼠标指针移出某元素时执行脚本       |
| onmouseover | 脚本 | 当鼠标指针悬停于某元素之上时执行脚本 |
| onmouseup   | 脚本 | 当鼠标按钮被松开时执行脚本           |



### 八、结构化

- 使用恰当的文档类型声明和命名空间。
- 使用 meta 元素声明你的内容类型。
- 使用小写字母书写所有的元素和属性。
- 为所有的属性值加引号。
- 为所有的属性分配值。
- 关闭所有的标签。
- 使用空格和斜线关闭空标签。
- 不要在注释中写双下划线。
- 确保小于号及和号为 < 和 &
- 为表达语义而标记文档，而不是为了样式：最大限度地使用 CSS 来进行布局
	- 根据它们的意义使用元素，而不是根据它们的外观
	- 使用结构化元素，而不是无意义的垃圾 ：ul、li
- div、id 和其他帮手

