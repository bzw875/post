---
title: 8位浮点数所有值
date: {{ date }}
updated: {{ date }}
tags:
categories:
---
下面的页面会显示8位浮点数所出现的个数。
第1个位是符号位
第2到第5位是指数
后面3位是有效数字。

计算得到0到255个浮点数

```html
// html
<!DOCTYPE html>
<html>
<head>
<title></title>
</head>
<body>
<style>
#show {
    position: relative;
    width: 1024px;
    height: 1px;
    background-color: black;
}
.item {
    position: absolute;
    top: 0;
    left: 0;
    width: 1px;
    height: 20px;
    background-color: red;
}
</style>
<div id="show">
    <div class="item"></div>
</div>
<script type="text/javascript">
/*
0 0000 000
0-256
*/
function run(power){
    var arr = [];
    var all = Math.pow(2, power)
    for (var i = 0; i < all; i++) {
        var str = i.toString(2);
        if (str.length < power) {
            str = str.padStart(power, '0')
        }
        var num = floatStr(str);
        if (num !== null) {
            arr.push(num);
        }
    }
    return arr;
}

function renderFloat(arr) {
    arr.forEach(num => {
        var show = document.getElementById('show')
        var div = document.createElement('div');
        div.className = 'item';
        div.style.left = (num * 2 + 512) + 'px';
        show.appendChild(div);
    });
}

renderFloat(run(8));


// 0 1111 000
function floatStr(str) {
    str = str.replace(/\\s/g, '');
    var V = str[0] === '0' ? 1 : -1;
    var E = str.slice(1,5);
    var M = str.slice(-3);

    if (E === '0000') {
        E = 1 - 7;
        M = parseInt(M, 2);
        return V * M * Math.pow(2, E - 3);
    }
    else if (E === '1111') {
        return null;
        if (M === '000') {
            return V === 1 ? Number.MAX_VALUE : Number.MIN_VALUE;
        } else {
            return NaN;
        }
    }
    else {
        E = parseInt(E, 2) - 7;
        M = parseInt(M, 2);
        M = M === 0 ? 1 : Math.pow(M, -3) + 1;
        return V * M * Math.pow(2, E);
    }
}
</script>
</body>
</html>
```
