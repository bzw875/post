---
title: JavaScript实现康威生命游戏
date: 2022-09-06 15:39:51
updated: 2022-09-06 15:39:51
tags:
categories:
---


### 演示demo
[生命游戏](https://raw.githack.com/bzw875/GameOfLife/master/00.html)

### 定义

康威生命游戏（英语：Conway's Game of Life），又称康威生命棋，是英国数学家约翰·何顿·康威在1970年发明的细胞自动机。
它最初于1970年10月在《科学美国人》杂志上马丁·葛登能的“数学游戏”专栏出现。


### 规则
生命游戏中，对于任意细胞，规则如下：

* 每个细胞有两种状态 - 存活或死亡，每个细胞与以自身为中心的周围八格细胞产生互动（黑色为存活，白色为死亡）
* 当前细胞为存活状态时，当周围的存活细胞低于2个时（不包含2个），该细胞变成死亡状态。（模拟生命数量稀少）
* 当前细胞为存活状态时，当周围有2个或3个存活细胞时，该细胞保持原样。
* 当前细胞为存活状态时，当周围有超过3个存活细胞时，该细胞变成死亡状态。（模拟生命数量过多）
* 当前细胞为死亡状态时，当周围有3个存活细胞时，该细胞变成存活状态。（模拟繁殖）

可以把最初的细胞结构定义为种子，当所有在种子中的细胞同时被以上规则处理后，可以得到第一代细胞图。按规则继续处理当前的细胞图，可以得到下一代的细胞图，周而复始。


### 规则用代码表示
``` javascript
假如有个生命
var a = { x: 4, y: 4 }
// 周围存活数为
var n = neighborLifeNumber();

// 当前细胞为存活状态时，当周围的存活细胞低于2个时（不包含2个），该细胞变成死亡状态。
if (n < 2 && a.isLeft) {
    a.isLeft = false;
}

// 当前细胞为存活状态时，当周围有2个或3个存活细胞时，该细胞保持原样
if (n === 2 || n === 3 && a.isLeft) {
    // 什么也不做
}

// 当前细胞为存活状态时，当周围有超过3个存活细胞时，该细胞变成死亡状态。（模拟生命数量过多）
if (n > 3 && a.isLeft) {
    a.isLeft = false;
}


// 当前细胞为死亡状态时，当周围有3个存活细胞时，该细胞变成存活状态。（模拟繁殖）
if (n >= 3 && !a.isLeft) {
    a.isLeft = true;
}
```

### 核心算法就是
* 假设现存的生命为 left
* 根据 left 算计出邻居生命 neighbor (这里面有很多重复的生命)
* 算出 neighbor 生命出现的次数并去重，得出 frequency
* 从 frequency 过滤出现3次的生命得出 newLife（因为不管是死是活都会在下一轮转为活）
* 从 frequency 过滤出现2次的生命得出 countIsTwo
* 从 countIsTwo 、 left 算出同时出现的生命 nowlife ，这个是旧left因为有2个邻居而活下来的生命
* 合并 newLife 、 nowlife得出下一轮活的生命


### github 地址
[github.com/bzw875/GameOfLife](https://github.com/bzw875/GameOfLife)

### 完整代码

``` javascript
// 怎么使用
new CellLife({
  width: 100, // 网格宽度
  height: 100, // 网格高度
  initialNumber: 500, // 初始化生命个数
  cycleTime: 200, // 生命更新毫秒数
  box: document.getElementById('root')
});

// 构造类

class CellLife {
    constructor(options) {
        const { width, height, cycleTime, initialNumber, box} = options;
        this.width     = width;
        this.height    = height;
        this.cycleTime = cycleTime;
        this.initialNumber = initialNumber;
        this.box = box;

        this.life = this.createCellByRandom();
        this.createCheckerboard();
    }
    tick (callback) {
        var newLife = this.updateCell();
        callback(newLife);
        if (newLife.length === 0) {
            callback([]);
        }
    }

    updateCell () {
        const neighbor   = this.findNeighbor(this.life);
        const frequency  = this.countFrequency(neighbor, this.life);
        const newLife    = this.filterCountIsThree(frequency);
        const countIsTwo = this.filterCountIsTwo(frequency);
        const nowlife    = this.mergeNewLifeAndSurvive(newLife, countIsTwo, this.life);
        this.life = nowlife;
        return nowlife;
    }

    createCellByRandom () {
        const life = new Set();
        while (life.size < this.initialNumber) {
            life.add({
                x: Math.floor(Math.random() * this.width),
                y: Math.floor(Math.random() * this.height)
            });
        }
        return [...life];
    }

    findNeighbor (life) {
        const allNeighbor = [];
        life.forEach(cell => allNeighbor.push(...this.neighborCell(cell.x, cell.y)));
        return allNeighbor;
    }

    neighborCell (self_x, self_y) {
        const neighbor = [];
        const that = this;
        [-1, 0, 1].forEach(function(i) {
            [-1, 0, 1].forEach(function(j) {
                const x = self_x + i;
                const y = self_y + j;
                if (that.isValidCell(x, y, self_x, self_y)) {
                    neighbor.push({ x, y });
                }
            });
        });
        return neighbor;
    }

    isValidCell (x, y, self_x, self_y) {
        return x >= 0 && y >= 0 && x < this.width && y < this.height && (self_x !== x || self_y !== y);
    }

    countFrequency (neighbor) {
        var mapCell = {};
        const frequency = [];
        var len = neighbor.length;
        for (var i = 0; i < len; i++) {
            var ele = neighbor[i];
            var sameEle = mapCell[ele.x+''+ele.y];
            if (sameEle) {
                sameEle.count += 1;
            } else {
                sameEle = {
                    x: ele.x,
                    y: ele.y,
                    count: 1
                };
                mapCell[ele.x+''+ele.y] = sameEle;
                frequency.push(sameEle);
            }
        }
        mapCell = null;
        return frequency;
    }

    filterCountIsThree (frequency) {
        return frequency.filter(cell => cell.count === 3);
    }

    filterCountIsTwo (frequency) {
        return frequency.filter(cell => cell.count === 2);
    }

    mergeNewLifeAndSurvive (newLife, countIsTwo, life) {
        var len,
            ele,
            mapCell = {},
            survive = [];

        
        len = life.length;
        for (var i = 0; i < len; i++) {
            ele = life[i];
            mapCell[ele.x+''+ele.y] = ele;
        }

        
        len = countIsTwo.length;
        for (var i = 0; i < len; i++) {
            ele = countIsTwo[i];
            if (mapCell[ele.x+''+ele.y]) {
                survive.push(ele);
            }
        }

        return [...newLife, ...survive];
    }
    createCheckerboard(){
        var td = new Array(this.height+5).join( '<tr>'+(new Array(this.width+5)).join('<td></td>')+'</tr>' );
        var table = '<table><tbody>'+td+'</tbody></table>';
        this.box.innerHTML = table;

        var table = this.box.querySelector('tbody');
        var tds = table.querySelectorAll('td');
        var trs = table.querySelectorAll('tr');

        clearInterval(this.timer);
        this.timer = setInterval(()=> {
            this.tick(life =>{
                
                tds.forEach((ele, i)=>{
                    ele.className = '';
                });
                
                for (var i = 0, len = life.length; i < len; i++) {
                    var cell = life[i];
                    trs[cell.y+2].children[cell.x+2].className = 'life';
                }
                if (life.length === 0) {
                    clearInterval(this.timer);
                }
                
            });
            
        }, this.cycleTime);
    }

    destroy() {
        this.box.innerHTML = '';
        clearInterval(this.timer);
    }
}
```