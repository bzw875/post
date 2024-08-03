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

## 微信红包算法
 - 所有人抢到金额之和等于红包总金额，不能超过，也不能少于；
 - 抢到的红包金额至少是一分钱；
 - 要保证抢到红包的人获取到的红包金额是随机的。

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


## js 实现两个字符串数字相加（大数相加）

我面试抖音的面试题，中等难度

``` javascript
const addStr = (num1, num2) => {
  const len = Math.max(num1.length, num2.length);
  const str1 = num1.padStart(len, '0')
  const str2 = num2.padStart(len, '0')
  const result = [];
  for (let i = len - 1; i >= 0; i--) {
    result.push(parseInt(str1[i] || 0) + parseInt(str2[i] || 0));
  }
  return result.reverse().join('');
};
console.log(addStr('123454321', '456'))
```

## 八皇后问题

八皇后问题，是一个古老而著名的问题，是 回溯算法 的典型案例。

该问题是国际西洋棋棋手马克斯·贝瑟尔于 1848 年提出：在 8×8 格的国际象棋上摆放八个皇后，使其不能互相攻击，即：任意两个皇后都不能处于同一行、同一列或同一斜线上，问有多少种摆法。

使用回溯算法，高斯认为有 76 种方案。1854年在柏林的象棋杂志上不同的作者发表了 40 种不同的解，后来有人用图论的方法解出 92 种结果

``` javascript
function hasConflict(row, column, queens) { //  判断是否与已摆放的皇后冲突
    return queens.some(a => a[0] === row) || // 同一行
           queens.some(a => a[1] === column) || // 同一列
           queens.some(a => Math.abs(a[0] - row) === Math.abs(a[1] - column)); // 同斜线
}
function printQ(queens){ //   打印结果
    const str = Array.from({ length: 8 }, () => Array(8).fill('-'));
    queens.forEach(a => {
        str[a[0]][a[1]] = 'Q';
    })
    console.log(str.map(a => a.join(' ')).join('\n'))
}
let count = 0;
function find_queen(row, queens) { // 递归放置皇后
    if (row === 8) { // 棋盘放满了，记录结果
        count++;
        console.log('Eight Queens Solve ' +count)
        printQ(queens);
        return;
    }
    for(let column = 0; column < 8; column++) {
        if (!hasConflict(row, column, queens)) {
            queens.push([row, column]);
            find_queen(row+1, queens); // 可以放置，接下来继续放置下一行
            queens.pop(); //  回溯算法 最最重要！！！
        }
    }
}
find_queen(0, []);
```

## 爬楼梯
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

``` JavaScript
const cache = {};
const climbStairs = (n) => {
  if (n === 1) {
    return 1;
  }
  if (n === 2) {
    return 2;
  }
  if (n === 3) {
    return 3;
  }
  if (cache[n]) {
    return cache[n];
  }
  const a = climbStairs(n - 1)
  const b = climbStairs(n - 2);
  cache[n] = a + b;
  return a + b;
}
console.log( climbStairs(46))
```

## 移动零
使用双指针，j指针填充的位置，遇到0停下，然后填充i指针

``` javascript
const moveZeroes = (nums) => {
    //第一次遍历的时候，j指针记录非0的个数，只要是非0的统统都赋给nums[j]
    let j = 0;
    for(let i=0;i<nums.length;++i) {
        if(nums[i]!=0) { // 和上一个对调
            nums[j++] = nums[i];
            console.log(nums.join(' '))
        }
    }
    //非0元素统计完了，剩下的都是0了
    //所以第二次遍历把末尾的元素都赋为0即可
    for(let i=j;i<nums.length;++i) {
        nums[i] = 0;
    }
    return nums;
}
console.log(moveZeroes([0,1,0,3,12])) // [1, 3, 12, 0, 0]
```