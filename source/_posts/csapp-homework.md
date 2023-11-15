---
title: 深入理解计算机系统（csapp）作业解答
date: {{ date }}
updated: {{ date }}
tags:
categories:
---

# 第二部分
## 第二章
2.55 实现show_bytes
2.56 试着用不同的值运行show_bytes
``` c
#include <stdio.h>
#include <stdlib.h>

typedef unsigned char *byte_pointer;

void show_bytes(byte_pointer a, int len) {
int i;
	for(i=0; i<len; i++) {
		printf("%.2x ", a[i]);
	}
	printf("\\n");
}
int main() {
    int a = 123456789;
    printf("show int %d\\n", a);
    show_bytes((byte_pointer)&a, sizeof(a));
    return 0;
}
```
2.57 编写show_short, show_long, show_double
``` c
#include <stdio.h>
#include <stdlib.h>

typedef unsigned char *byte_pointer;

void show_bytes(byte_pointer a, int len) {
int i;
	for(i=0; i<len; i++) {
		printf("%.2x ", a[i]);
	}
	printf("\\n");
}
void show_short(short s)
{
    printf("the value of short %d is:", s);
    show_bytes((char *)&s, sizeof(short));
}

void show_long(long long l)
{
    printf("the value of short %lld is:", l);
    show_bytes((char *)&l, sizeof(long long));
}

void show_double(double d)
{
    printf("the value of short %lf is:", d);
    show_bytes((char *)&d, sizeof(double));
}


int main() {
    short a = 8;
    show_short(a);
    long b = 12345678;
    show_long(b);
    double c = 1234.5678;
    show_double(c);
    return 0;
}
```
2.58 实现is_little_endian
``` c
#include <stdio.h>

typedef unsigned char *byte_pointer;

int is_little_endian()
{
    int val = 0x00000001;
    byte_pointer valp = (byte_pointer)&val;
    int temp;
    temp = valp[0];
    if (temp == 1)
        return 1;
    else
        return 0;
}

int main()
{
    int result = is_little_endian();
    printf("is_little_endian: %d", result);
    return 1;
}
```
2.59生成一个字，由X的最低有效字节和y剩下的字节组成
``` c
#include <stdio.h>

typedef unsigned char *byte_pointer;

void show_bytes(byte_pointer a, int len)
{
    int i;
    for (i = 0; i < len; i++)
    {
        printf("%.2x ", a[i]);
    }
    printf("\\n");
}

int main()
{
    int x = 0x89ABCDEF;
    int y = 0x76543210;
    int z = (x & 0xFF) | (y & ~0xFF);
    show_bytes((byte_pointer)&z, sizeof(z));
    return 1;
}
```
2.60
将一个w位的字中的字节从0到w/8-1编号，用C实现返回一个无符号值，其中参数x的字节i位被替换成字节b
``` c
#include <stdio.h>
#include <inttypes.h>

typedef unsigned char *char_point;

uint32_t replace_byte(uint32_t x, int i, unsigned char b)
{
    if (i > 3 || i < 0)
    {
        return -1;
    }

    char_point char_date_point = ((char_point)&x) + i;

    *char_date_point = b;

    printf("result : %X\\r\\n", x);
    return x;
}

int main(void)
{
    unsigned char replace_data = 0xAB;

    uint32_t x = 0x12345678;
    uint32_t r_x = 0x12AB5678;
    int i_x = 2;

    uint32_t y = x;
    uint32_t r_y = 0x123456AB;
    int i_y = 0;

    printf("r_x == result : %d\\r\\n", r_x == replace_byte(x, i_x, replace_data));
    printf("r_y == result : %d\\r\\n", r_y == replace_byte(y, i_y, replace_data));

    return 1;
}
```