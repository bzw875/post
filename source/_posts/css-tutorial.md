---
title: CSS简单教程
date: 2019-04-21 14:18:47
updated: 2019-04-21 14:18:47
tags: CSS
categories:
---

# 一、常用css属性
## (1) *block（区块）
行高 line-height:数值 | inherit | normal;

字间距 letter-spacing: 数值 | inherit | normal;

词间距 word-spacing: 数值 | inherit | normal;

空格 white-space: pre(保留) | nowrap(不换行) | normal;

```
/*表格宽度自适应*/
th {
white-space: nowrap;
}
```
### 显示
```
display:none; /*不显示，使用的场景非常多*/
    block; /*把内联标签变成块级标签*/
    inline; /*把块级标签变成内联标签*/
    list-item; /*列表项*/
    run-in; /*追加部分*/
    compact; /*紧凑*/
    marker; /*标记*/
    table;
    inline-table;
    table-raw-group;
    table-header-group;
    table-footer-group;
    table-raw;
    table-column-group;
    table-column;
    table-cell;
    table-caption; /*表格标题*/
```
## (2) *box（盒子）
宽度 width: 长度 | 百分比 | auto;

高度 height: 长度 | 百分比 | auto;

清除 clear: none | left | right | both;

边界 margin: 上 右 下 左 ;

填充 padding: 上 右 下 左 ;

定位 position: absolute | relative | static;

透明度 visibility: inherit | visible | hidden;

溢出 overflow: visible | hidden | scroll auto;

裁切 clip: rect(12px,auto,12px,auto)

## (3) float（漂浮）
漂浮 float: left | right | none; 在页面布局的时候用的最多

常见用法
```
<div style='background-color:red;float:left;width: 50%;' >div1</div>
<div style='background-color:green;float:right;width: 50%;' >div2</div>
```
一个问题
子标签使用了float时候，父标签的样式失效

```
<div style='background-color:red;'>
    <div style="float: left">div1</div>
    <div style="float: left">div2</div>
</div>
```

解决方案一：clear: both

```
<div style='background-color:red;'>
    <div style="float: left">div1</div>
    <div style="float: left">div2</div>
    <div style="clear: both;"></div> <!--加上clear：both之后就正常了-->
</div>
```
解决方案二：clearfix
```
<div style='background-color:red;' class="clearfix">
    <div style="float: left">div1</div>
    <div style="float: left">div2</div>
</div>
.clearfix:after{
    content: ".";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}
```
## (4) position（定位）
fixed
一般用来写网页顶端的固定导航条，或者两侧的菜单。

```
<!--对于块级标签来说加上position:fixed之后，该div就不会占一整行，一般需要手动定义宽度，如width:100%-->
 
<div style="position:fixed;height:10%;background-color:lightskyblue;color:white;width:100%;top:0px;">我是导航</div>
<div style="">
    <div style="position:fixed;bottom: 0px;top:10%;float: left;width: 20%;background-color:indianred">我是菜单</div>
    <div style="float: right;width:80%;"><p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
        <p>我是内容</p>
    </div>
</div>
```
absolute与relative
这两者一般配合使用，用于调整div之间的相对位置
```
<div style="position:relative;width: 300px;height: 150px;">
    <div style="position:absolute;float: left;width: 20%;background-color:indianred;bottom: 0px;right: 0px;">我是菜单</div>
</div>

```
## (5) 透明度
```
.image{
    opacity: 0.5
}
<img src="http://www.jotlab.com/wp-content/uploads/2008/08/python.jpg" style="opacity: 0.5; width:50%; height:50%; ">
```
## (6) font（字体）
```
颜色 color: 数值;
大小 font-size: 数值;
字体 font-family: "Courier New", Courier, monospace, "Times New Roman", Times, serif, Arial, Helvetica, sans-serif, Verdana
样式 font-style: oblique;(偏斜体) italic;(斜体) normal;(正常)
粗细 font-weight: bold;(粗体) lighter;(细体) normal;(正常)
变体 font-variant: small-caps;(小型大写字母) normal;(正常)
```
## (4) background（背景）
```
背景 background: transparent; /透视背景*/
颜色 background-color: 数值;
图片 background-image: url() | none;
重复 background-repeat: inherit | no-repeat | repeat | repeat-x | repeat-y;

background-repeat : repeat; /*重复排列-网页默认*/
background-repeat : no-repeat; /*不重复排列*/
background-repeat : repeat-x; /*在x轴重复排列*/
background-repeat : repeat-y; /*在y轴重复排列*/
滚动 background-attachment: fixed | scroll;
位置 background-position:数值 | top | bottom | left | right | center;

background-position : 90% 90%; /*背景图片x与y轴的位置*/
background-position : top; /*向上对齐*/
background-position : buttom; /*向下对齐*/
background-position : left; /*向左对齐*/
background-position : right; /*向右对齐*/
background-position : center; /*居中对齐*/
简写 background:背景颜色 | 背景图象 | 背景重复 | 背景附件 | 背景位置 ;
```
## (7) text（文本）
```
大小写 text-transform: capitalize | uppercase | lowercase | none;
修饰 text-decoration: underline;(下划线) overline;(上划线) line-through;(删除线) blink;(闪烁)
排列 text-align: justify | left | right | center;
缩进 text-indent: 数值 | inherit;
阴影 text-shadow:数值;
```

## (8) border（边框）
```
边框样式 border-style: dotted;(点线) dashed;(虚线) solid; double;(双线) groove;(槽线) ridge;(脊状) inset;(凹陷) outset;
边框宽度 border-width: ;
边框颜色 border-color: top值 right值 bottom值 left值;
简写 border: width style color;

边　　框 {border:border-width border-style color}
上 边 框 {border-top:border-top-width border-style color}
右 边 框 {border-right:border-right-width border-style color}
下 边 框 {border-bottom:border-bottom-width border-style color}
左 边 框 {border-left:border-left-width border-style color}
```
## (9) list-style（列表样式）
```

类型 list-style-type: disc | circle | square | decimal | lower-roman | upper-roman | lower-alpha | upper-alpha | none;

list-style-type:none; /*不编号*/
list-style-type:decimal; /*阿拉伯数字*/
list-style-type:lower-roman; /*小写罗马数字*/
list-style-type:upper-roman; /*大写罗马数字*/
list-style-type:lower-alpha; /*小写英文字母*/
list-style-type:upper-alpha; /*大写英文字母*/
list-style-type:disc; /*实心圆形符号*/
list-style-type:circle; /*空心圆形符号*/
list-style-type:square; /*实心方形符号*/
位置 list-style-position: outside | inside;
图像 list-style-image: URL;
简写 list-style:目录样式类型 | 目录样式位置 | url;
```
## (10) margin（边界）

```
margin-top:10px; (上边界)
margin-right:10px; (右边界)
margin-bottom:10px; (下边界值)
margin-left:10px; (左边界值)
margin-inside:;
margin-outside:;

```
## (11) padding（填充）
```
padding-top:10px; /*上边框留空白*/
padding-right:10px; /*右边框留空白*/
padding-bottom:10px; /*下边框留空白*/
padding-left:10px; /*左边框留空白
```
## (12) vertical（垂直）
```
vertical-align:sub; /*下标字*/
vertical-align:super; /*上标字*/
vertical-align:top; /*垂直向上对齐*/
vertical-align:bottom; /*垂直向下对齐*/
vertical-align:middle; /*垂直居中对齐*/
vertical-align:text-top; /*文字垂直向上对齐*/
vertical-align:text-bottom; /*文字垂直向下对齐*/
```
## (13) a（链接）
```
a /*所有超链接*/
a:link /*超链接文字格式*/
a:visited /*浏览过的链接文字格式*/
a:active /*按下链接的格式*/
a:hover /*鼠标转到链接*/
```
## (14) cursor（光标）
```
光标形状 cursor:hand | crosshair | text | wait | move | help | e-resize | nw-resize | w-resize | s-resize | se-resize | sw-resize;

/*也可以自定义*/
cursor: hand; /*链接手指*/
cursor: crosshair /*十字体 */
cursor: s-resize /*箭头朝下 */
cursor: move /*十字箭头, 朝右*/
cursor: help /*加一问号 */
cursor: w-resize /*箭头朝左 */
cursor: n-resize /*箭头朝上 */
cursor: ne-resize /*箭头朝右上 */
cursor: nw-resize /*箭头朝左上 */
cursor: text /*文字型*/
cursor: se-resize /*箭头斜右下 */
cursor: sw-resize /*箭头斜左下*/
cursor: wait /*漏斗*/
```
# 二、css实践
## (1) css的三种写法
行内样式：写在对应标签的style属性里面
```
<html>
    <head>  
        <title>Test</title>
    </head>

    <body>
        <div style='background-color:red'>123</div>
    </body>
</html>
```
内页样式：写在HTML页面里面的style标签里面
```
<html>
    <head>
        <title>Test</title>
        <style>
            .logo{
                background-color:red;
            }
        </style>
    </head>

    <body>
        <div class='logo'>123</div>
    </body>
</html>

```
外部样式：通过link标签引入CSS样式

```
<html>
    <head>
        <title>Test</title>
        <link rel='stylesheet' href='common1.css'/>
    </head>

    <body>
        <div class="logo">123</div>
    </body>
</html>
.logo {
    background-color: red;
    color: white;
}
```
## (2) 常规用例
```
p {font-family: "sans serif";}  /*值为若干单词，则要给值加引号*/

.logo {background-color: red;}

.logo a,.logo p {background-color: red;}

#morra {background-color: green;}

a, div { color: red;}   /*a或div都使用这个css*/

a div { color: red;}    /*只有a下面的div使用该css*/
```
注：css 对大小写不敏感。不过存在一个例外：如果涉及到与 HTML 文档一起工作的话，class 和 id 名称对大小写是敏感的。

三、Demo
```
<!DOCTYPE html>
<html>
<head>
    <title>This is a demo</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <style type="text/css">
        body {
            background-color: #e1ddd9;
            font-size: 12px;
            font-family: Verdana, Arial, Helvetica, SunSans-Regular, Sans-Serif;
            color: #564b47;
            padding: 0px;
            margin: 0px;
        }
        #inhalt {
            position: absolute;
            height: 200px;
            width: 400px;
            margin: -100px 0px 0px -200px;
            top: 50%;
            left: 50%;
            text-align: center;
            padding: 0px;
            background-color: #f5f5f5;
            border: 1px dotted #000000;
            overflow: auto;
        }
        p, h1 {
            margin: 0px;
            padding: 10px;
        }
        h1 {
            font-size: 11px;
            text-transform: uppercase;
            text-align: center;
            color: #564b47;
            background-color: #90897a;
        }
        a {
            color: #ff66cc;
            font-size: 11px;
            background-color: transparent;
            text-decoration: none;
        }
    </style>
</head>
<body>
<div id="inhalt">
    <p>
    <h1>Morra's Demo</h1><br/><br/>
    This area should be horizontally and vertically centered.<br/>
    This text stays left aligned<br/>
    <a href="http://www.cnblogs.com/whatisfantasy/">what is fantasy?</a>
    </p>
    <p>
</div>
</body>
</html>
```


# 盒模型
盒模型(box model)是CSS中的一个重要概念，它是元素大小的呈现方式。需要记住的是："every element in web design is a rectangular box"。如图：

box-model
![](D:/work/front-end-tutorial/box-sizing.png)

CSS3中新增了一种盒模型计算方式：```box-sizing```熟悉。盒模型默认的值是content-box, 新增的值是```padding-box```和```border-box```，几种盒模型计算元素宽高的区别如下：

## content-box（默认）
布局所占宽度Width：
```
Width = width + padding-left + padding-right + border-left + border-right
```
布局所占高度Height:
```
Height = height + padding-top + padding-bottom + border-top + border-bottom
```
## padding-box
布局所占宽度Width：
```
Width = width(包含padding-left + padding-right) + border-top + border-bottom
```
布局所占高度Height:
```
Height = height(包含padding-top + padding-bottom) + border-top + border-bottom
```
## border-box
布局所占宽度Width：
```
Width = width(包含padding-left + padding-right + border-left + border-right)
```
布局所占高度Height:
```
Height = height(包含padding-top + padding-bottom + border-top + border-bottom)
```
## margin叠加
外边距叠加是一个相当简单的概念。 但是，在实践中对网页进行布局时， 它会造成许多混淆。 简单的说， 当两个或更多个垂直边距相遇时， 它们将形成一个外边距。这个外边距的高度等于两个发生叠加的外边距的高度中的较大者。但是注意只有普通文档流中块框的垂直外边距才会发生外边距叠加。 行内框、 浮动框或绝对定位框之间的外边距不会叠加。

一般来说， 垂直外边距叠加有三种情况：

* 元素自身叠加 当元素没有内容（即空元素）、内边距、边框时， 它的上下边距就相遇了， 即会产生叠加（垂直方向）。 当为元素添加内容、 内边距、 边框任何一项， 就会取消叠加。
* 相邻元素叠加 相邻的两个元素， 如果它们的上下边距相遇，即会产生叠加。
* 包含（父子）元素叠加 包含元素的外边距隔着 父元素的内边距和边框， 当这两项都不存在的时候， 父子元素垂直外边距相邻， 产生叠加。 添加任何一项即会取消叠加。


# CSS普通流（文档流）
首先明确一点的是，W3C规范中没有document flow这个概念，只有normal-flow, 文档流的叫法主要还是多数中文译者的翻译方式问题。

## 定义
什么是普通流？简单说就是元素按照其在 HTML 中的位置顺序决定排布的过程。并且这种过程遵循标准的描述。

## 调节普通流元素位置
一般使用margin是用来隔开元素与元素的间距；padding是用来隔开元素与内容的间隔。margin用于布局分开元素使元素与元素互不相干；padding用于元素与内容之间的间隔，让内容（文字）与（包裹）元素之间有一段“距离”。

只要不是float和绝对定位方式布局的，都在普通流里面。

# CSS定位方式
## display属性
每一个元素都有默认的display属性，使用最多的是block, inline和inline-block，不常用的是table-cell。

根据display属性，我们可以将元素分为块级元素(block)和内联级元素(inline)。它们最大区别是:block元素可以设置宽度，独占一行。inline元素宽度由内容决定，与其他元素并列在一行。

常见的block属性元素有：div, h1-h6, ul, li, ol, dl, dd, dt。

常见的inline属性元素有: span, a, em。

## block
宽高可以自行设置，默认宽度由父容器决定，默认高度有内容决定。自己独占一行。

## inline
宽度和高度都有内容决定，与其他元素共占一行。

## inline-block
宽度可以自行设置，类似block，但是与其他元素共占一行，类似inline。长用于设置垂直居中。

## table-cell
此属性指让标签元素以表格单元格的形式呈现，单元格有一些比较特殊的属性，可以设置元素的垂直居中等。

# position属性
元素在页面中的布局遵守一套文档流的方式，默认的定位属性值为static。它其实是未被设置定位的。

元素如果被定位了，那么它的top,left,bottom,right值就会生效，能设置定位的属性是relative,absolute和fixed。

需要注意的另一点是被定位的元素层次(z-index)会得到提高。

## relative（相对定位）
设置了相对定位之后，通过修改top,left,bottom,right值，元素会在自身文档流所在位置上被移动，其他的元素则不会调整位置来弥补它偏离后剩下的空隙。

## absolute（绝对定位）
设置了绝对定位之后，元素脱离文档流，其他的元素会调整位置来弥补它偏离后剩下的空隙。元素偏移是相对于是它最近的设置了定位属性（position值不为static）的元素。

且如果元素为块级元素（display属性值为block)，那么它的宽度也会由内容撑开。因为：

默认文档流中块级元素如果没有设置宽度属性，会自动填满整行。

## fixed(固定定位)
设置了固定定位之后，元素相对的偏移的参考是可视窗口，即使页面滚动，元素仍然会在固定位置。


# CSS浮动相关
这也是CSS定位机制的一种。

首先了解两个概念：

文档流：文档流是文档中可显示对象在排列时所占用的位置。
* 浮动的定义：使元素脱离文档流，按照指定方向发生移动，遇到父级边界或者相邻的浮动元素停了下来。
* 浮动的实际用途，可设置文字环绕或使元素宽度由内容填充（类似Inline-block)。使用浮动需要注意的是如果浮动的元素高度比父级容器还高，那么需要设置父级容器的overflow属性为auto,使其自动撑满。


[清除浮动](http://www.iyunlu.com/view/css-xhtml/55.html)


# CSS选择器
选择器是匹配元素的一种模式，不只是在CSS中，JavaScript对CSS的选择器也是支持的，比如document.document.querySelectorAll。

## 关于CSS解析器
HTML 经过解析生成 DOM Tree（这个我们比较熟悉）；而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。

Render Tree 中的元素（WebKit 中称为「renderers」，Firefox 下为「frames」）与 DOM 元素相对应，但非一一对应：一个 DOM 元素可能会对应多个 renderer，如文本折行后，不同的「行」会成为 render tree 种不同的 renderer。也有的 DOM 元素被 Render Tree 完全无视，比如 display:none 的元素。

在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 renderer。对于每个 DOM 元素，必须在所有 Style Rules 中找到符合的 selector 并将对应的规则进行合并。选择器的「解析」实际是在这里执行的，在遍历 DOM Tree 时，从 Style Rules 中去寻找对应的 selector。

## 解析顺序
CSS匹配不是从左到右进行查找，而是从右到左进行查找。如果从左到右的顺序，那么每条选择器都需要遍历整个DOM树，性能很受影响。所谓高效的CSS就是让浏览器在查找style匹配的元素的时候尽量进行少的查找, 所以选择器最好写的简洁一点。

## 选择器权重
权重，也就是选择器的优先级，每条选择器的规则都有其权重，权重大的会覆盖掉权重小的，很多CSS出现问题的场景，都是某处定义了一个更高权重的规则，导致此处规则不生效。

根据样式所在位置，对元素的影响也有关系：内联样式（标签内style形式） > style标签 > link标签。

另外一点需要注意的是!improtant,凡是属性值后加上了!important，那么它的值不会被其他值替换。

权重的计算
通过这篇文章你应该知道的一些事情——CSS权重。了解下权重的计算，主要的规则就是:

id选择器 > 类，属性选择器和伪类选择器 > 元素和伪元素

## 基本选择器
通配符选择器（＊）
id选择器（\\#ID）
类选择器（.className）
元素选择器(E)
后代选择器（Ｅ Ｆ）
子元素选择器(E>F)
相邻兄弟元素选择器(E + F)
群组选择器（selector1,selector2,...,selectorN）
属性选择器
使用CSS3属性选择器，你可以只指定元素的某个属性，或者你还可以同时指定元素的某个属性和其对应的属性值。

E[attr]：只使用属性名，但没有确定任何属性值
E[attr="value"]：指定属性名，并指定了该属性的属性值
E[attr~="value"]：指定属性名，并且具有属性值，此属性值是一个词列表，并且以空格隔开，其中词列表中包含了一个value词，而且等号前面的“〜”不能不写
E[attr^="value"]：指定了属性名，并且有属性值，属性值是以value开头的；
E[attr$="value"]：指定了属性名，并且有属性值，而且属性值是以value结束的；
E[attr*="value"]：指定了属性名，并且有属性值，而且属值中包含了value；
E[attr|="value"]：指定了属性名，并且属性值是value或者以“value-”开头的值（比如说zh-cn）;
## 伪类选择器
伪类选择器的形式就是:xxx， 比如:hover, :link, :nth。

## 动态伪类
这些伪类并不存在于HTML中,而只有当用户和网站交互的时候才能体现出来，动态伪类包含两种，第一种是我们在链接中常看到的锚点伪类，如":link",":visited";另外一种被称作用户行为伪类，如“:hover”,":active"和":focus"。先来看最常见的锚点伪类。

hover: 用于当用户把鼠标移动到元素上面时的效果
active: 用于用户点击元素那一下的效果（正发生在点的那一下，松开鼠标左键此动作也就完成了）
focus: 用于元素成为焦点，这个经常用在表单元素上
## UI元素状态伪类
主要是针对于HTML中的Form元素操作, IE8不支持":checked",":enabled",":disabled"这三种选择器。

## CSS3的:nth选择器
主要注意的是CSS3添加的nth选择器在IE8下不支持。

fist-child: 选择某个元素的第一个子元素；
last-child: 选择某个元素的最后一个子元素；
nth-child(): 选择某个元素的一个或多个特定的子元素；
其他： 常用的就是上面三种了，其他自行了解。
选择器分类总结

见图:

css-selector
![](D:/work/front-end-tutorial/css-selector.jpg)
选择器兼容性
选择器的兼容性:

css选择器兼容性
![](D:/work/front-end-tutorial/cssSelect2.jpg)
选择器的优化