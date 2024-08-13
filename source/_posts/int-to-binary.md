---
title: js实现整数转二进制原码、补码
date: 2021-07-12 09:44:19
updated: 2021-07-12 09:44:19
tags: 计算机科学
categories:
---

为了加强对原码，反码，补码的理解，写了一个js函数整型转原码二进制的函数，同时支持反码和补码

 - 原码就是符号位加上真值的绝对值
 - 反码是正数的反码是其本身；负数的反码是在其原码的基础上，符号位不变，其余各个位取反
- 补码是正数的补码就是其本身；负数的补码是在其原码的基础上，符号位不变，其余各位取反，最后+1。(也即在反码的基础上+1)



``` javascript

const int_to_binary = (num, size, type) => {
    size = size || 64; // 大小默认64位
    type = type || 0; // 0 原码、1 反码、2 补码
    const negative = num < 0; // 符号
    const reverseAndNegative = type === 1 && negative;
    const arr = new Array(size).fill(reverseAndNegative ? '1' : '0');
    let cur = Math.abs(num);
    if (type === 2 && negative) {
        cur += 1;
    }
    let j = size - 1;
    while (cur !== 0) {
        const remainder = cur % 2;
        cur = (cur - remainder) / 2;
        if (reverseAndNegative) {
            arr[j] = remainder === 0 ? '1' : '0';
        } else {
            arr[j] = remainder;
        }
        j--;
        if (j < 0) {
            throw 'overflow'
        } 
    }
    arr[0] = negative ? '1' : '0';
    return arr.join('');
};
console.log(int_to_binary( 123, 16, 0)) // 00000000000000000000010011010010
console.log(int_to_binary(-123, 16, 0)) // 10000000000000000000010011010010
console.log(int_to_binary( 123, 16, 1)) // 01111111111111111111101100101101
console.log(int_to_binary(-123, 16, 1)) // 11111111111111111111101100101101
console.log(int_to_binary( 123, 16, 2)) // 00000000000000000000010011010010
console.log(int_to_binary(-123, 16, 2)) // 10000000000000000000010011010011

```
