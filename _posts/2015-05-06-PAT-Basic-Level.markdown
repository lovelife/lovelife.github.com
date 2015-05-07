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
> 题意：任意一个不超过1000的正整数n,偶数则减半，奇数则3*n+1再减半，求多少步变成1.
> 
> Key：直接按题意计算，十分简单。

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
> 题意：给一个自然数n，n小于10^100,计算各位数字之和，按拼音输出。
> 样例：
> >1234567890987654321123456789
> >yi san wu
> 
> Key：把n的每一位相加得到sum，再根据sum的每一位，输出对应数字拼音.

```c
#include<stdio.h>

int main()
{
    char n[102] = {0};
    scanf("%s",n);
    
    int i = 0, sum = 0;  // sum:[0,909]
    while(n[i])
    {
        sum += n[i] - '0';
        i++;
    }
    
    char *str[] = {"ling","yi","er","san","si","wu","liu","qi","ba","jiu"};
    if( sum / 100) printf("%s ",str[sum/100]);
    if( sum / 100 || (sum / 10) % 10 ) printf("%s ",str[(sum/10)%10]);
    printf("%s",str[sum%10]);
    return 0;
}
```

>[1003. 我要通过！(20)][3]
>
> 题意：给定字符串满足下面条件则答案正确输出YES，否则输出NO.
> 1. 字符串中必须仅有P, A, T这三种字符，不可以包含其它字符；
> 2. 任意形如 xPATx 的字符串都可以获得“答案正确”，其中 x 或者是空字符串，或者是仅由字母 A 组成的字符串；
> 3. 如果 aPbTc 是正确的，那么 aPbATca 也是正确的，其中 a, b, c 均或者是空字符串，或者是仅由字母 A 组成的字符串。
>
>Key: 根据xPATx正确，aPbTc在b=A,a=c的情况下正确
>而aPbTc正确，则aPbATca正确，则aPbAATcaa正确，依次aPbTc有每次b后扩展一个A则c后扩展一个a
>即有aPbA...ATca...a也正确（前后省略个数相同）且aPbA...ATca...a ＝ aPAA...ATaa...a
>以上可概括为：
>>**字符串中只有P、A、T**
>>**P在前T在后，各只出现一次**
>>**P前的A个数＊PT间A的个数＝T后面A的个数, PT间A的个数至少有1个**
>>
>

```c
#include<stdio.h>
int ispat(char *strpat)
{
    char *p = 0,*t = 0,*str = strpat;
    int pre_A,mid_A,end_A;
    
    while(*str)
    {
        if(*str == 'P')
        {
            if(!p) p = str;
            else return 0;
            
        }
        else if(*str == 'T')
        {
            if(!t) t = str;
            else return 0;
            
        }
        else if(*str != 'A')
        {
            return 0;
        }
        str++;
    }
    
    if(p >= t) return 0;
    
    pre_A = p - strpat;
    mid_A = t - p - 1;
    end_A = str - t - 1;
    
    if( mid_A < 1 || (pre_A*mid_A) != end_A) return 0;
    
    return 1;
}
int main()
{
    int n;
    scanf("%d",&n);
    
    char str[101] = {0};
    while(n--)
    {
        scanf("%s",str);
        
        if(ispat(str))printf("YES\n");
        else printf("NO\n");
    }
    
    return 0;
}
```


[1]:http://www.patest.cn/contests/pat-b-practise/1001
[2]:http://www.patest.cn/contests/pat-b-practise/1002
[3]:http://www.patest.cn/contests/pat-b-practise/1003