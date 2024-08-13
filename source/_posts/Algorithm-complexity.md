---
title: 算法复杂度JavaScript例子
date: 2023-07-22 10:12:58
updated: 2023-07-22 10:12:58
tags: 算法 leetcode
categories:
---

算法的时间复杂度是用来描述算法运行时间与输入数据规模之间的关系

空间复杂度是输入数据和内存使用的关系，这里就不详细说，看[空间复杂度百科](https://baike.baidu.com/item/%E7%A9%BA%E9%97%B4%E5%A4%8D%E6%9D%82%E5%BA%A6)

### 常数时间复杂度 O(1)
常数时间复杂度意味着无论输入大小如何，执行时间都是固定的。

``` Javascript
function addFive(n) {
    return n + 5;
}
console.log(addFive(10)); // 输出: 15
```
### 线性时间复杂度 O(n)
线性时间复杂度意味着执行时间与输入规模成正比。

``` Javascript
function linearTime(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}
console.log(linearTime([1, 2, 3, 4, 5])); // 输出: 15
```
### 对数时间复杂度 O(log n)
对数时间复杂度通常出现在每次迭代可以排除一半的可能性的情况，例如二分查找。

``` Javascript
function binarySearch(sortedArray, target) {
    let left = 0;
    let right = sortedArray.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        if (sortedArray[mid] === target) {
            return mid;
        } else if (sortedArray[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}
const sortedArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```
console.log(binarySearch(sortedArray, 7)); // 输出: 6
### 平方时间复杂度 O(n^2)
当一个算法需要遍历所有可能的元素组合时，可能会出现平方时间复杂度。

``` Javascript
function quadraticTime(arr) {
    let result = 0;
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length; j++) {
            result += arr[i] * arr[j];
        }
    }
    return result;
}
console.log(quadraticTime([1, 2, 3])); // 输出: 35
```
### 指数时间复杂度 O(2^n)
指数时间复杂度通常出现在递归算法中，比如求解斐波那契数列。

``` Javascript
function fibonacci(n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}
console.log(fibonacci(5)); // 输出: 5


// 解决办法可以用缓存，把已知的结果换成起来，如果有缓存则不用重复计算
const cache = {};
function fibonacciWithCache(n) {
    if (n <= 1) {
        return n;
    }
    if (cache[n]) {
        return cache[n];
    }
    const next = fibonacciWithCache(n - 1);
    const next2 = fibonacciWithCache(n - 2);
    cache[n - 1] = next;
    cache[n - 2] = next2;
    return next + next2;
}
```