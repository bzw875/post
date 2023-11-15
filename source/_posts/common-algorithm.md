---
title: 常见算法
date: {{ date }}
updated: {{ date }}
tags:
categories:
---

## 斐波那次数列
``` javascript
// 节省内存空间，没有重复计算
function fibonacci(n){
	if (n < 2) {
		return;
	}
	let tmp1 = 1;
	let tmp2 = 1;
	let tmp3;
	for (var i = 1; i < n; i++) {
		tmp3 = tmp1 + tmp2;
		tmp1 = tmp2;
		tmp2 = tmp3;
	}
	return tmp3;
}
console.log(fibonacci(9))
```


## 快速排序

``` javascript
function quickSort(arr) {
    // 交换
    function swap(arr, a, b) {
    	console.log('swap ' + arr[a] + '   ' + arr[b])
        var temp = arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }

    // 分区
    function partition(arr, left, right) {
        /**
         * 开始时不知最终pivot的存放位置，可以先将pivot交换到后面去
         * 这里直接定义最右边的元素为基准
         */
        var pivot = arr[right];
        /**
         * 存放小于pivot的元素时，是紧挨着上一元素的，否则空隙里存放的可能是大于pivot的元素，
         * 故声明一个storeIndex变量，并初始化为left来依次紧挨着存放小于pivot的元素。
         */
        var storeIndex = left;
        for (var i = left; i < right; i++) {
            if (arr[i] < pivot) {
                /**
                 * 遍历数组，找到小于的pivot的元素，（大于pivot的元素会跳过）
                 * 将循环i次时得到的元素，通过swap交换放到storeIndex处，
                 * 并对storeIndex递增1，表示下一个可能要交换的位置
                 */
                swap(arr, storeIndex, i);
                storeIndex++;
            }
        }
        // 最后： 将pivot交换到storeIndex处，基准元素放置到最终正确位置上
        swap(arr, right, storeIndex);

    	console.log('storeIndex ' + storeIndex)
        return storeIndex;
    }

    function sort(arr, left, right) {
        if (left > right) return;

        /*
        	以最后一个为标准，比它小的移动到前面，
        	存储一个index。index最后一个是它，前面是比它小的数。
        */
        var storeIndex = partition(arr, left, right);
        // 然后依次递归调用index左边和右边的项
        sort(arr, left, storeIndex - 1);
        sort(arr, storeIndex + 1, right);
    }

    sort(arr, 0, arr.length - 1);
    return arr;
}
```

## 二叉树

``` javascript
class Node {
  constructor(key) {
    this.key = key;
    this.left = null;
    this.right = null;
  }
}
class BinarySearchTree {
  constructor(keys) {
    this.root = null;
    keys.forEach((key) => {
      let newNode = new Node(key)
      if (this.root === null) {
        this.root = newNode
      } else {
        this.insertNode(this.root, newNode)
      }
    })
  }
  insertNode(node, newNode) {
    if (newNode.key < node.key) {
      if (node.left === null) {
        node.left = newNode
      } else {
        this.insertNode(node.left, newNode)
      }
    } else {
      if (node.right === null) {
        node.right = newNode
      } else {
        this.insertNode(node.right, newNode)
      }
    }
  }
  traverse(node, order, callback) {
    if (node !== null) {
      order === 'root-left-right' && callback(node.key);
      this.traverse(node.left, order, callback)
      order === 'left-root-right' && callback(node.key);
      this.traverse(node.right, order, callback)
      order === 'left-right-root' && callback(node.key);
    }
  }
  findMin () {
  	let node = this.root;
  	while (node.left) {
  		node = node.left;
  	}
  	return node.key;
  }
  findMax () {
  	let node = this.root;
  	while (node.right) {
  		node = node.right;
  	}
  	return node.key;
  }
}
/*
  8
 /  \\
 3   10
/ \\   \\
1 6    14
 / \\   /
4   7 13
*/

const keys = [8, 3, 10, 1, 6, 14, 4, 7, 13];
const tree = new BinarySearchTree(keys);
tree.traverse(tree.root, 'left-right-root', (key) => {
  console.log(key);
});
console.log('————');
console.log('findMin: ' + tree.findMin());
console.log('findMax: ' + tree.findMax());

```

微信红包算法
``` javascript
const MIN_AMOUNT = 2; // 最小红包
const MAX_AMOUNT = 40; // 最大红包
const luckyPackages = (num, total) => {
    const result = new Array(num);
    result.fill(MIN_AMOUNT);
    let remainder = total - (num * MIN_AMOUNT);
    while(remainder > 0) {
        const ran = Math.random();
        const i = Math.floor(num * ran);
        const split = remainder < 1 ? remainder
             : Number(((remainder/4) * ran).toFixed(1));

        if ((result[i] + split) <= MAX_AMOUNT) {
            result[i] += split;
            remainder -= split;
        } else {
            remainder -= MAX_AMOUNT - result[i];
            result[i] = MAX_AMOUNT;
        }
    }
    result.forEach((n, i) => {
        result[i] = Number(n.toFixed(1))
    });
    console.log(result.reduce((total, num) => {
        return total + Number(num);
    }, 0))
    console.log(result.join(', '));
};
luckyPackages(20, 200);
```