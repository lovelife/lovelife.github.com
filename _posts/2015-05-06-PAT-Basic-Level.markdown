---
layout: post
title: "PAT Basic Level Practice(1001-1010)"
description: "PAT乙级考试练习题"
categories:
- PAT

tags:
- acm
- 

---


>[1001.害死人不偿命的(3n+1)猜想 (15)][1]
>
> 水题，很简单

~~~c 
#include <stdio.h>

int main(int argc, char *argv[]) 
{
    int n, s = 0;
    scanf("%d",&n);
    
    while (n!=1) 
    {
        n = n%2 ? (3*n+1) / 2 : n / 2;
        s++;
    }
    printf("%d",s);
    
    return 0;
}
~~~

> [1002.写出这个数 (20)][2]
> 
> 水题，很简单
> 
> 把n的每一位相加得到sum，再根据sum的每一位，输出对应数字拼音.

```c
```

>[1003. 我要通过！(20)][3]

	1. 字符串中必须仅有P, A, T这三种字符，不可以包含其它字符；
	2. 任意形如 xPATx 的字符串都可以获得“答案正确”，其中 x 或者是空字符串，或者是仅由字母 A 组成的字符串；
	3. 如果 aPbTc 是正确的，那么 aPbATca 也是正确的，其中 a, b, c 均或者是空字符串，或者是仅由字母 A 组成的字符串。

>
>
>
>

```c
#includ<stdio.h>

int main()
{
    
    return 0;
}
```


[1]:http://www.patest.cn/contests/pat-b-practise/1001
[2]:http://www.patest.cn/contests/pat-b-practise/1002
[3]:http://www.patest.cn/contests/pat-b-practise/1003