---
layout: post
title: "PAT Basic Level Practice"
description: "PAT乙级考试练习题"

categories:
- PAT


tags:
- acm 


---

## [1001]

> 害死人不偿命的(3n+1)猜想 (15)
> 
> 水题,简单


#include <stdio.h>

int main(int argc, char *argv[]) 
{
    int n, s = 0;
    scanf("%d",&n);

    while (n!=1) {
        n = n%2 ? (3*n+1) / 2 : n / 2;
        s++;
    }
    printf("%d",s);
}

[1001]:http://www.patest.cn/contests/pat-b-practise/1001
