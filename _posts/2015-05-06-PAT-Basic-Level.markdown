---
layout: post
title: "PAT Basic Level Practice"
description: "PAT乙级考试练习题"

categories:
- PAT


tags:
- acm 


---

#1001

````
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
````