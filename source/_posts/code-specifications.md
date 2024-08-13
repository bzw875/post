---
title: 前端代码规范和最佳实践
date: 2020-05-04 16:43:01
updated: 2020-05-04 16:43:01
tags: 前端
categories:
---

# HTML

### 语法

* 缩进使用soft tab（4个空格）；
* 嵌套的节点应该缩进；
* 在属性上，使用双引号，不要使用单引号；
* 不要在自动闭合标签结尾处使用斜线（HTML5 规范 指出他们是可选的）；`<img src="">`
* 不要忽略可选的关闭标签，例：</li> 和 </body>。

### HTML5 doctype

    <!DOCTYPE html>

* 在页面开头使用这个简单地doctype来启用标准模式，使其在每个浏览器中尽可能一致的展现；
* 虽然doctype不区分大小写，但是按照惯例，doctype大写 （关于html属性，大写还是小写）。


#### lang属性

根据HTML5规范：应在html标签上加上lang属性。这会给语音工具和翻译工具帮助，告诉它们应当怎么去发音和翻译。

比如

    <html lang="zh-cn">
    <html lang="en-us">
    
    
### 字符编码

    <meta charset="UTF-8">
    
通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为'UTF-8'。


### IE兼容模式
* 用 <meta> 标签可以指定页面应该用什么版本的IE来渲染；
* 不同doctype在不同浏览器下会触发不同的渲染模式，所以别别忽略文档类型


### 标准的HTML5页面应该是这样

    <!DOCTYPE html>
    <html lang="zh-cn">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <meta http-equiv="X-UA-Compatible" content="IE=Edge">
    </head>
    <body>
        
    </body>
    </html>
    

### 引入CSS, JS

根据HTML5规范, 通常在引入CSS和JS时不需要指明 type，因为 text/css 和 text/javascript 分别是他们的默认值

    <link rel="stylesheet" href="code_guide.css">
    <script src="code_guide.js"></script>
    

### boolean属性

boolean属性指不需要声明取值的属性，XHTML需要每个属性声明取值，但是HTML5并不需要；
    
    <-- Good -->
    <input type="text" disabled>
    
    <input type="checkbox" value="1" checked>
    
    <select>
        <option value="1" selected>1</option>
    </select>
    
    <-- Bad -->
    <input type="text" disabled="disabled">
    
    <input type="checkbox" value="1" checked="checked">
    
    <select>
        <option value="1" selected>1</option>
    </select>
    

### 减少标签数量

    <-- Good -->
    <label class="uiLabel">
        &{'administrationgroup.code'}:
    </label>
    <input class="uiComponent" type="text"/>
        
    <-- Bad -->
    <span>
        <label class="uiLabel">
            &{'administrationgroup.code'}:
        </label>
        <span class="uiComponent">
            <input type="text"/>
        </span>
    </span>
    

# javascript

### 缩进
使用soft tab（4个空格）。


### 单行长度

不要超过80，但如果编辑器开启word wrap可以不考虑单行长度。


### 分号

以下几种情况后需加分号：

* 变量声明
* 表达式
* return
* throw
* break
* continue
* do-while



    var x = 1;
    
    x++;
    
    return;
    
    throw new Error('timeout');
    
    break;
    
    continue;

    do {
        x++;
    } while (x < 10);
    

### 换行

换行的地方，行末必须有','或者运算符；

以下几种情况不需要换行：

* 下列关键字后：`else, catch, finally`
* 代码块'{'前


以下几种情况需要换行：

* 代码块'{'后和'}'前
* 变量赋值后


    // not good
    var a = {
        b: 1
        , c: 2
    };
    
    x = y
        ? 1 : 2;
    
    // good
    var a = {
        b: 1,
        c: 2
    };
    
    x = y ? 1 : 2;
    x = y ?
        1 : 2;
    
    // no need line break with 'else', 'catch', 'finally'
    if (condition) {
        ...
    } else {
        ...
    }
    
    try {
        ...
    } catch (e) {
        ...
    } finally {
        ...
    }
    
    // not good
    function test()
    {
        ...
    }
    
    // good
    function test() {
        ...
    }
    
    // not good
    var a, foo = 7, b,
        c, bar = 8;
    
    // good
    var a,
        foo = 7,
        b, c, bar = 8;


### 引号
最外层统一使用单引号。

    // Good
    function foo (data) {
        return '<a href="#" onclick="clickFn(\\''+data.id+'\\')"></a>'
    }
    
    // bad
    function foo (data) {
        return "<a href='#' onclick='clickFn(\\'"+data.id+"\\')'></a>"
    }


### 括号

下列关键字后必须有大括号（即使代码块的内容只有一行）：`if, else, for, while, do, switch, try, catch, finally, with`。


    // not good
    if (condition)
        doSomething();
    
    // good
    if (condition) {
        doSomething();
    }

### 建议使用 && 、 || 、！!(obj)、三元运算符等

    if(data && data.length) //这是合理的判断，&&是依次判断，遇否中断， 建议
    var name = data.name || ''; //依次都判断，遇true赋值，建议
    var isName = names.split(',').lenght > 1 ? '名称正确'： '名称错误';
    var isCanvas = !!(canvas.getContext('2d'));

### 请使用字面量值创建对象

    // Good
    var obj = {};
    var users = [];
    var str = 'abc';
    var num = 1;
    var isDefault = false;
    
    // bad
    var obj = new Object();
    var users = new Array();
    var str = new String('abc');
    var num = new Number(1);
    var isDefault = new Boolean(false);


### 别使用javascript 关键字和保留字

    // 比如 class 是保留字
    var obj = {
        name: 'userid',
        class: 'text-left'
    };

### 只调用一次的函数就别单独声明了

    function getData () {
        $.get('/abc', getDataCallback)
    }
    function getDataCallback (data) {
        console.log(data);
    }
    
    function getData () {
        $.get('/abc', function  (data) {
            console.log(data);
        })
    }
    

关键字

    break
    case
    catch
    continue
    default
    delete
    do
    else
    finally
    for
    function
    if
    in
    instanceof
    new
    return
    switch
    this
    throw
    try
    typeof
    var
    void
    while
    with

保留字

    abstract
    boolean
    byte
    char
    class
    const
    debugger
    double
    enum
    export
    extends
    final
    float
    goto
    implements
    import
    int
    interface
    long
    native
    package
    private
    protected
    public
    short
    static
    super
    synchronized
    throws
    transient
    volatile
    
### 不要使用 eval()

* eval 太神秘了，以至于很多人用错。所以不推荐使用
* 说到性能问题，在旧的浏览器中如果你使用了eval，性能会下降10倍

 
setInterval和setTimeout 传递字符串也是变相使用eval

    setInterval('foo()', 100)


    
    
    
### 不用switch

* 容易漏掉break
* 没有 if else 清晰
* 

### 不要用setAttribute 修改元素的布尔类型的属性

**根据官方的建议：具有 true 和 false 两个属性的属性，这些checked、 selected、 readonly、 disabled、 autocomplete、autoplay、loop、muted、preload、autofocus、required、open 使用prop()，其他的使用 attr()**

    // bad
    $option.attr('selected', 'selected'); // jquery 的方法
    option.setAttribute('selected', 'selected'); 原生的方法
    
    // good
    $option.prop('selected', true); // jquery 的方法
    option.selected = true; 原生的方法

### jQuery最佳实践

[jQuery最佳实践](http://www.ruanyifeng.com/blog/2011/08/jquery_best_practices.html)





# 最后

推荐你们都读一遍或者多遍这本书，里面有javascript最好的实践。
公司有购买的在书架上

![Alt text](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1521780545495&di=b26fccd445887ce52807fb3bfa3a43bd&imgtype=0&src=http%3A%2F%2Fec4.images-amazon.com%2Fimages%2FI%2F511yJOQpxvL.jpg)