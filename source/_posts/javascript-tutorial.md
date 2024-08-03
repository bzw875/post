---
title: javascript简单教程
date: 2019-02-19 13:27:35
updated: 2019-02-19 13:27:35
tags:
categories:
---

# 事件概述

## DOM0级事件处理程序

> 通过Javascript指定事件处理程序的传统方式，就是将一个函数赋值给一个事件处理程序属性。
每个元素都有自己的事件处理程序属性，这些属性通常全部小写，例如onclick。将这种属性的值设置为一个函数，就可以指定事件处理程序。

``` javascript
// HTML 写法
<button onclick="foo()"></button>

// js 写法
var btn = document.getElementById('myBtn');
// 添加事件处理程序
btn.onclick = function () {
    alert( this );//为DOM元素btn
};
// 移除事件处理程序
btn.onclick = null;
```

**优点:**
1.简单
2.具有跨浏览器的优势

**缺点:**
在代码运行之前不会指定事件处理程序，因此这些代码在页面中位于按钮后面，就有可能在一段时间怎么点击都没反应，用户体验变差。


## DOM2级事件处理程序

> 定义了两个方法，用于处理指定和删除事件处理程序的操作:addEventListener()和removeEventListener()。三个参数，1.要处理的事件名。2.作为事件处理程序的函数3.一个布尔值。最后这个布尔值为true,表示在捕获阶段调用事件处理程序，false表示在冒泡阶段调用事件处理程序。

``` javascript
// 添加多个事件处理程序
var btn = document.getElementById('myBtn');
btn.addEventListener('click',function (){
    alert( this );// 为DOM元素btn
},false );
btn.addEventListener('click',function () {
    alert('Hello World');
},false);

// 移除事件处理程序
btn.removeEventListener('click',function () {
    // 匿名函数无法被移除,移除失败
},false);
// 改写
var handler = function () {
    alert(this.id);
};
btn.addEventListener('click',handler,false);
// 再次移除事件处理程序
btn.removeEventListener('click',handler,false);
// 移除成功
```

这两个事件处理程序会按照添加他们的顺序触发。大多数情况，都是将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度的兼容各种版本的浏览器。

**优点:**
 一个元素可以添加多个事件处理程序
 
 **缺点:**
 IE8及以下浏览器不支持DOM2级事件处理程序。(包括IE8)
 
 
 # 事件对象
 
> 兼容DOM的浏览器会将一个event对象传入到事件处理程序中。无论指定事件处理程序时使用什么方法(DOM0级或DOM2)级，都会传入event对象。event对象包含与创建它的特定事件有关的属性和方法。触发的事件类型不一样，可用的属性和方法也不一样。不过，所有事件都有下表列出的成员


属性/方法 | 类型 | 说明
------------ | ------------- | ------------
bubbles  | 属性 |  返回一个布尔值，如果事件是起泡类型，则返回 true，否则返回 fasle
canceble   | 属性 |  返回布尔值，指示事件是否可拥可取消的默认动作
target   | 属性 |  事件的目标对象
currentTarget  | 属性 |  其当前事件处理程序正在处理事件的那个元素
defaultPrevented 属性 |  |  表明当前事件是否调用了 event.preventDefault()方法
evnetPhase  | 属性 |  返回事件传播的当前阶段没处理：0、捕获阶段: 1、正常事件派发: 2、起泡阶段: 3
preventDefault  | 方法 |  	通知浏览器不要执行与事件关联的默认动作如submit动作
stopPropagation  | 方法 |  不再派发事件
isTrusted   | 属性 |  返回一个布尔值,为true表明当前事件是由用户行为触发
type  | 属性 |  读属性 Event.type 会返回一个字符串, 表示该事件对象的事件类型


# DOM 操作

### DOM选择

``` javascript
// DOM操作jquery和原生

// css 选择器
var ele = document.querySelector('.someCLass'); // 单个元素
var ele = document.querySelectorAll('.someCLass'); // 多个元素
var ele = document.getElementById('someId'); // 通过ID获取
var ele = document.getElementsByClassName('some-class') // 通过class获取
var ele = document.getElementsByTagName('div') // 通过标签获取
var $ele = $('#someId')

```
注释
下面ele表示元素DOM，$ele表示jquery对象

### 元素特性
``` 布尔类型的属性
// 原生
ele.disabled
ele.readonly
ele.checked
ele.selected
// jquery
$ele.prop('disabled') // getter
$ele.prop('disabled', true) // settter

```

### 元素特性
``` 元素特性-原生
ele.id
ele.value
ele.className
ele.title

// 使用点号
ele.id
ele.id = 'otherId'
ele.id = ''

// 也可以使用 getAttribute setAttribute removeAttribute
ele.getAttribute('id')
ele.setAttribute('id', 'abcId')
ele.removeAttribute('id')

// 元素特性-jquery
$ele.attr('id')
$ele.attr('id', 'abcId')
$ele.removeAttr('id')
```

### 添加元素
``` javascript
// 设置元素的HTML
ele.innerHTML = '<div>123</div>'
$ele.html('<div>123</div>')

// 插入子元素
var div = document.createElement('div');
ele.insertBefore(div, null); // 插入最后面
ele.insertBefore(div, ele.firstElementChild); // 插入最前面

var div2 = document.createElement('div');
$ele.append(div2); // 插入最后面
$ele.prepend(div2); // 插入最前面
```

### 创建元素
``` javascript
var div = document.createElement('div');
var div = $('<div></div>');
```

### 移除元素
``` javascript
// 清空元素的HTML
ele.innerHTML = ''
$ele.html('')
$ele.empty('')

// 原生
ele.remove();

// jquery
$ele.remove();
```

### 操作元素的class
``` javascript
ele.className // 因为class是js的关键字
ele.className = 'someClass'
var classList = ele.classList;

classList.add('abc')
classList.remove('abc')
classList.toggle('abc') //类存在，则删除它并返回false，如果不存在，则添加它并返回true
classList.contains('abc') //是否包含abc

// jquery
$ele.addClass('abc')
$ele.removeClass('abc')
$ele.toggleClass('abc')
$ele.hasClass('abc')
```

### 操作元素的文本
``` javascript
ele.textContent // get
ele.textContent = 'some text' // set
$ele.text()
$ele.text('some text')
```

### 节点关系API
``` javascript
// 父节点
ele.parentElement
$ele.parent()

// 子节点
ele.children 子节点
ele.firstChild 第一个子节点
ele.lastChild 最后一个子节点


$ele.children()
$ele.children('div:first-child')
$ele.children('div:last-child')
```

### 兄弟关系API
``` javascript
ele.previousElementSibling 同一级前一个子节点
ele.nextElementSibling 同一级后一个子节点

// jquery类似的
$ele.prev()
$ele.next()
```

### 修改样式
``` javascript
window.getComputedStyle(ele, 'color') // 获取样式
ele.style.color = 'red' // 设置样式


$ele.css('color')
$ele.css('color', 'red');
$ele.css({ // 多个样式
    'color': 'red',
    'fontSize': '14px'
})
```