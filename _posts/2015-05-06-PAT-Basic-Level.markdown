---
layout: post
title: "PAT Basic Level Practice"
description: "PAT乙级考试练习题"

categories:
- PAT


tags:
- acm 


---

#### [1001.害死人不偿命的(3n+1)猜想 (15)][1001]
[1001]:http://www.patest.cn/contests/pat-b-practise/1001

> 
> 水题，简单
> 

{% highlight c %}
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
{% endhighlight %}


#### [1002.写出这个数 (20)][1002]
[1002]:http://www.patest.cn/contests/pat-b-practise/1002

>
> 水题，简单
> 把n的每一位相加得到sum，再根据sum的每一位，输出对应数字拼音
> 
{% highlight c %}
#include <stdio.h>

int main(int argc, char *argv[]) 
{
    char n[102] = {0};
    int sum = 0, i = 0;
    char *str[]={"ling","yi","er","san","si","wu","liu","qi","ba","jiu"};
    
    scanf("%s",n);
    while(n[i])
    {
        sum = sum + n[i] - '0';
        i++;
    }   
    
    if(sum/100) printf("%s %s %s",str[sum/100],str[(sum/10)%10],str[sum%10]);
    else if((sum/10)%10 ) printf("%s %s",str[(sum/10)%10],str[sum%10]);
    else printf("%s",str[sum%10]);     
           
    return 0;
}

{% endhighlight %}
