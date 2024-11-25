---
title: 前端面试写代码题
date: 2024-01-09 16:00:24
updated: 2024-01-09 16:00:24
tags: 面试题
categories:
---

## 修改console.log前面加上时间戳
``` javascript
(function(){
    const oldLog = console.log;
    console.log = function(...arr){
        arr.unshift((new Date()).toISOString())
        oldLog.apply(console, arr);
    }
})()

console.log(1.1,'2', null, {a:33})
// 2024-08-22T02:09:53.124Z 1.1 2 null {a: 33}
```

## 数组转成树形层级


#### 非递归解法算法复杂度2n
``` javascript
function toTree(arr){
    const idMap = {}; // 所有节点
    const childMap = {}; // 所有子节点
    arr.forEach((item)=> {
        idMap[item.id] = item;
        if (item.parentId) {
            childMap[item.parentId] = childMap[item.parentId] || [];
            childMap[item.parentId].push(item);
        }
    })
    arr.forEach((item)=> {
        if (item.parentId) {
            idMap[item.parentId].children = childMap[item.parentId];
        }
    })

    return arr.filter(item => item.parentId === null);
}
const arr = [
    { id: 5, name: 'node 5', parentId: null },
    { id: 4, name: 'node 4', parentId: 2 },
    { id: 3, name: 'node 3', parentId: 4 },
    { id: 2, name: 'node 2', parentId: 5 },
    { id: 1, name: 'node 1', parentId: null }
];
console.log(JSON.stringify(toTree(arr), null, 2));
// 打印
[
  {
    "id": 5,
    "name": "node 5",
    "parentId": null,
    "children": [
      {
        "id": 2,
        "name": "node 2",
        "parentId": 5,
        "children": [
          {
            "id": 4,
            "name": "node 4",
            "parentId": 2,
            "children": [
              {
                "id": 3,
                "name": "node 3",
                "parentId": 4
              }
            ]
          }
        ]
      }
    ]
  },
  {
    "id": 1,
    "name": "node 1",
    "parentId": null
  }
]
```


#### while循环解法
``` javascript
function toTree(arr){
    const parentNode = arr.filter(tmp => tmp.parentId === null);
    const other = arr.filter(tmp => tmp.parentId !== null);

    let i = 0;
    let max = arr.length*100;
    while(other.length > 0) {
        const tmp = other[i];
        const p = findParent(parentNode, tmp.parentId)
        if (p) {
            p.children = p.children || [];
            p.children.push(tmp);
            other.splice(i, 1);
        }
        if (i >= other.length - 1) {
            i = 0;
        } else {
            i++;
        }
        max--;
        if (max === 0) {
            throw("parentId not found: " + tmp.parentId);
        }
    }
    return parentNode;
}

function findParent(arr, parentId) {
    for (let i = 0; i < arr.length; i++) {
        const tmp = arr[i];
        if (tmp.id === parentId) {
            return tmp;
        }
        if (tmp.children) {
            const loop = findParent(tmp.children, parentId);
            if (loop) {
                return loop;
            }
        }
    }
}
```