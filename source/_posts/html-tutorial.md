---
title: HTML 简单教程
date: 2019-03-29 14:56:37
updated: 2019-06-20 10:00:27
tags: HTML
categories:
---


# HTML常用标签
## div
div标签用于组合其他HTML元素，本身无实在意义。常用于页面的布局，比如一个展开式的广告页面框架大致如下：
``` html
<body>
    <div id="wrap-container">
        <div id="collapsed-container"></div>
        <div id="expanded-container"></div>
    </div>
</body>
```

## h1~h6, p, span, strong, em...


此类标签用于设置文本，常见的使用方式是填充段落，比如弹出的legal框文字HTML结构如下:

``` html
<div id="legal-window">
    <h4>LEGAL</h4>
    <img id="legal-close" src="img/embed/legal-close.png" alt="close window">
    <p>*Requires a system with Intel<sup>&reg;</sup> Turbo Boost Technology. Intel<sup>&reg;</sup> Turbo Boost Technology and Intel<sup>&reg;</sup> Turbo Boost Technology 2.0 are only available on select Intel<sup>&reg;</sup> processors. Consult your PC manufacturer. Performance varies depending on hardware, software, and system configuration. For more information, visit http://www.intel.com/go/turbo. Copyright &copy; 2014 Intel Corporation. All rights reserved. Intel, the Intel logo, Intel Core, Look Inside, Intel Inside, and Pentium are trademarks of Intel Corporation in the U.S. and/or other countries. Other names and brands may be claimed as the property of others.</p>
</div>
```

## ul, li, ol, dl, dt, dd
此类标签用于设置带有列表内容的，比如导航栏的下拉菜单，多视频的缩略图等：

``` html
<ul class="nav-tools-list">
    <li>
        <div>
            <img src="shoppingtools-icon-1.png" alt="">
            <span>Build & Price</span>
        </div>
    </li>
    <li>
        <div>
            <img src="shoppingtools-icon-2.png" alt="">
            <span>Incentives & Offers</span>
        </div>
    </li>
</ul>

<dl>
   <dt>计算机</dt>
   <dd>用来计算的仪器 ... ...</dd>
   <dt>显示器</dt>
   <dd>以视觉方式显示信息的装置 ... ...</dd>
</dl>
```

## form表单相关
页面中涉及到表单时候，需要使用到form相关标签：
``` html
<form name="frm-sample" class="frm-sample" action="try" method="post">
    <input type="text" class="form-control" placeholder="Name">
    <div id="status-message"></div>
    <div id="sample-captcha"></div>
    <a id="check-is-filled" class="info-btn">Check if visualCaptcha is filled</a>
    <button type="submit" name="submit-bt" class="submit">Submit form</button>
</form>
```

## table表格相关
页面中涉及到table结构，需要使用到table相关标签:
``` html
<table></table>
```

## img, canvas

用于图像显示。一般不直接操作img,canvas元素，而是在它的外层包裹一层父级元素（可以为span,div等)，对父级元素进行操作：
``` html
<div class="preload" data-src="CheddarBacon.png">
    <img src="CheddarBacon.png" alt="">
</div>
<!-- or -->
<div id="sprite-car" class="cw-sprite sprite-car" cw-interval="30" cw-loops="1" cw-auto-play="false" cw-texture="images/sprites/expanded/car-texture.png" cw-mapper="car">
    <canvas class="cw-renderer" width="460" height="130"></canvas>
</div>
```

## a
a标签用于打开链接，发送邮件，段落跳转等功能。使用时需要注意阻止掉标签的默认事件。

链接跳转，常见的关于分享按钮的HTML结构如下：
``` html
<div id="shareBox">
    <ul>
        <li id="facebook">
            <a target="_blank" rel="nofollow" data-shareWay="facebook">
                <img alt="Post on Facebook" src="img/embed/f4Icon3.png" alt="Facebook" />
            </a>
        </li>
        <li id="twitter">
            <a target="_blank" rel="nofollow" data-shareWay="twitter">
                <img alt="Tweet this" src="img/embed/f4Icon4.png" />
            </a>
        </li>
        <li id="pinterest">
            <a data-pin-do="buttonPin" data-pin-config="none" target="_blank" rel="nofollow" data-shareWay="pinterest">
                <img alt="Pin it" src="img/embed/f4Icon5.png" />
            </a>
        </li>
        <li id="email">
            <a target="_blank" rel="nofollow" data-shareWay="email">
                <img src="img/embed/f4Icon6.png" />
            </a>
        </li>
    </ul>
    <p></p>
</div>
```
发送邮件的代码片段如下：
``` html
<div class="button">
  <a class="mail" data-img="mail.png" href="mailto:example@gmail.com?subject=xxx&body=xxx"></a>
</div>
```
段落跳转代码片段如下：
``` html
<div id="html5"></div>
<a name="user-content-html5" href="#html5" class="headeranchor-link" aria-hidden="true"><span class="headeranchor"></span></a>
```

## HTML5标签查询
[HTML MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element)


# HTML 常见属性


## HTML全局属性每个都有
### dir
规定元素中内容的文本方向。
### id
整个HTML文档中它的值必须是唯一的，名字不能重复。id值使用字符时，除了 ASCII字母和数字、“—”、“-"、"."之外，可能会引起兼容性问题，因为在HTML4中是不允许包含这些字符的，这个限制在HTML5中更加严格，为了兼容性id值必须由字母开头
### lang
规定元素内容的语言。
### style
规定元素的行内 CSS 样式。
### tabindex
规定元素的 tab 键次序、表单输入时按Tab键的切换顺序
[tabindex MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Global_attributes/tabindex)
### title
规定有关元素的额外信息。
### accesskey
规定激活元素的快捷键。
### class
用空格分开的一个或多个类名（引用样式表中的类）


## HTML5新属性
### contenteditable
规定元素内容是否可编辑。
### contextmenu
规定元素的上下文菜单。上下文菜单在用户点击元素时显示。
### data-*
用于存储页面或应用程序的私有定制数据。
### placeholder
属性提供一种提示（hint），描述输入域所期待的值
### draggable
规定元素是否可拖动。
### dropzone
规定在拖动被拖动数据时是否进行复制、移动或链接。
### hidden
规定元素仍未或不再相关。
### spellcheck
规定是否对元素进行拼写和语法检查。
### translate
规定是否应该翻译元素内容。



## 布尔属性要么true要么false
disabled
readonly
checked
selected
autocomplete


# HTML语义化

语义化的含义就是用正确的标签做正确的事情，html语义化就是让页面的内容结构化，便于对浏览器、搜索引擎解析；在没有样式CCS情况下也以一种文档格式显示，并且是容易阅读的。搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，利于 SEO。使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。


# DOCTYPE和浏览器渲染模式

文档类型，一个文档类型标记是一种标准通用标记语言的文档类型声明，它的目的是要告诉标准通用标记语言解析器，它应该使用什么样的文档类型定义（DTD）来解析文档。Doctype还会对浏览器的渲染模式产生影响，不同的渲染模式会影响到浏览器对于 CSS 代码甚至 JavaScript 脚本的解析，所以Doctype是非常关键的，尤其是在 IE 系列浏览器中，由DOCTYPE 所决定的 HTML 页面的渲染模式至关重要。

## 浏览器解析HTML方式
有三种解析方式:

* 非怪异（标准）模式
* 怪异模式
* 部分怪异（近乎标准）模式

在“标准模式”(standards mode) 页面按照 HTML 与 CSS 的定义渲染，而在“怪异模式(quirks mode) 模式”中则尝试模拟更旧的浏览器的行为。 一些浏览器（例如，那些基于 Mozilla 的 Gecko 渲染引擎的，或者 Internet Explorer 8 在 strict mode 下）也使用一种尝试于这两者之间妥协的“近乎标准”(almost standards) 模式，实施了一种表单元格尺寸的怪异行为，除此之外符合标准定义。

一个不含任何 DOCTYPE 的网页将会以 怪异(quirks) 模式渲染。

HTML5提供的<DOCTYPE html>是标准模式，向后兼容的, 等同于开启了标准模式，那么浏览器就得老老实实的按照W3C的 标准解析渲染页面，这样一来，你的页面在所有的浏览器里显示的就都是一个样子了。


# 理解DOM结构
DOM: Document Object Module, 文档对象模型。我们通过JavaScript操作页面的元素，进行添加、移动、改变或移除的方法和属性, 都是DOM提供的。

## W3C DOM 标准
被分为 3 个不同的部分:

核心 DOM - 针对任何结构化文档的标准模型
XML DOM - 针对 XML 文档的标准模型
HTML DOM - 针对 HTML 文档的标准模型
## DOM节点
根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点：

整个文档是一个文档节点
每个 HTML 元素是元素节点
HTML 元素内的文本是文本节点
每个 HTML 属性是属性节点
注释是注释节点

## HTML DOM 节点树
HTML文本会被解析为DOM树, 树中的所有节点均可通过 JavaScript 进行访问。所有 HTML 元素（节点）均可被修改，也可以创建或删除节点。

![](D:/work/front-end-tutorial/ct_htmltree.gif)

## 节点的关系
父（parent）、子（child）和同胞（sibling）等术语用于描述这些关系。父节点拥有子节点。同级的子节点被称为同胞（兄弟或姐妹）:

* 在节点树中，顶端节点被称为根（root）
* 每个节点都有父节点、除了根（它没有父节点）
* 一个节点可拥有任意数量的子
* 同胞是拥有相同父节点的节点
* 


![](D:/work/front-end-tutorial/dom_navigate.gif)


# HTML5新增内容
HTML5 是对 HTML 标准的第五次修订。其主要的目标是将互联网语义化，以便更好地被人类和机器阅读，并同时提供更好地支持各种媒体的嵌入。HTML5 的语法是向后兼容的。现在国内普遍说的 H5 是包括了 CSS3，JavaScript 的说法（严格意义上说，这么叫并不合适，但是已经这么叫开了，就将错就错了）。

## 与HTML 4的不同之处
文件类型声明（<!DOCTYPE>）仅有一型：<!DOCTYPE HTML>。
新的解析顺序：不再基于SGML。
新的元素：section, video, progress, nav, meter, time, aside, canvas, command, datalist, details, embed, figcaption, figure, footer, header, hgroup, keygen, mark, output, rp, rt, ruby, source, summary, wbr。
input元素的新类型：date, email, url等等。
新的属性：ping（用于a与area）, charset（用于meta）, async（用于script）。
全域属性：id, tabindex, repeat。
新的全域属性：contenteditable, contextmenu, draggable, dropzone, hidden, spellcheck。
移除元素：acronym, applet, basefont, big, center, dir, font, frame, frameset, isindex, noframes, strike, tt。
## 新增标签
HTML 5提供了一些新的元素和属性，反映典型的现代用法网站。其中有些是技术上类似``<div>``和``<span>``标签，但有一定含义，例如``<nav>``（网站导航块）和``<footer><audio>``和``<video>``标记。

## 移除的标签
一些过时的HTML 4标记将取消，其中包括纯粹用作显示效果的标记，如``<font>``和``<center>``，因为它们已经被CSS取代。还有一些通过DOM的网络行为。

## 修改的标签
尽管和SGML在标记上的相似性，HTML5的句法并不再基于它了，而是被设计成向后兼容对老版本的HTML的解析。它有一个新的开始列看起来就像SGML的文档类型声明，<!DOCTYPE HTML>，这会触发和标准兼容的渲染模式。在2009年1月5号，HTML5添加了Web Form 2.0的内容，html5开始发展起来。

## 无障碍（Accessibility）
为了使HTML5的新元素或新属性获取最大化的兼容性，开发人员需要附加一点额外补助，或者有些特性根本没有被任何浏览器实现，或者浏览器根本不支持补助技术。因此有些特殊的HTML5特性根本不能使用。更多细节可参见HTML5 Accessibility（无障碍）

## 新应用程序接口（API）
除了原先的DOM接口，HTML5增加了更多样化的API:

* HTML Geolocation
* HTML Drag and Drop
* HTML Local Storage
* HTML Application Cache
* HTML Web Workers
* HTML SSE
* HTML Canvas/WebGL 看demo"WebGL Demo.html"
* HTML Audio/Video


## 总结
最后奉上一张图片：

![](D:/work/front-end-tutorial/what-is-html5.jpg)

# 常用meta整理
## 概要
标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。

## 基本属性
| 属性 | 	值 | 	描述 |
| ------ | ------ | ------ |
| keywords | 	author / description / keywords / generator / revised / others | 	把 content 属性关联到一个名称。 |
| content | 	some text | 	定义与http-equiv或name属性相关的元信息 |
| http-equiv | 	content-type / expire / refresh / set-cookie | 	把content属性关联到HTTP头部。 |


# HTML 中有用的字符实体
![](D:/work/front-end-tutorial/entities.png)