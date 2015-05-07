---
layout: post
title: "PAT Basic Level Practice(1001-1040)"
description: "PAT乙级考试练习题"
categories:
- PAT

tags:
- acm


---

* [x] [1001](#ID1001) [1002](#ID1002) [1003](#ID1003) [1004](#ID1004) [1005](#ID1005)
* [x] [1006](#ID1006) [1007](#ID1007) [1008](#ID1008) [1009](#ID1009) [1010](#ID1010)
* [ ] [1011](#ID1011) [1012](#ID1012) [1013](#ID1013) [1014](#ID1014) [1015](#ID1015)
* [ ] [1016](#ID1016) [1017](#ID1017) [1018](#ID1018) [1019](#ID1019) [1020](#ID1020)
* [ ] [1021](#ID1021) [1022](#ID1022) [1023](#ID1023) [1024](#ID1024) [1025](#ID1025)
* [ ] [1026](#ID1026) [1027](#ID1027) [1028](#ID1028) [1029](#ID1029) [1010](#ID1030)
* [ ] [1031](#ID1031) [1032](#ID1032) [1033](#ID1033) [1034](#ID1034) [1035](#ID1035)
* [ ] [1036](#ID1036) [1037](#ID1037) [1038](#ID1038) [1039](#ID1039) [1040](#ID1040)

做题有个要点：读懂题意，然后用最快的速度、最简单直接的方法去解决问题。重构、优化代码那是后续的事，应该是先解决问题，然后再进一步优化。1001～1040题都简单，代码量也小，但是要拿一下拿满分也没那么容易。[1003](#ID1003)代码简单，但思路蛮难想到的。[1010](#ID1010)容易忽略0多项式的情形。

>
> <a id="ID1001"> 
> **[1001.害死人不偿命的(3n+1)猜想 (15)][1]**
> </a>
>
> **题意**：任意一个不超过1000的正整数n,偶数则减半，奇数则3*n+1再减半，求多少步变成1.
> 
> **解答**：直接按题意计算，十分简单。
>
> 

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

> <a id="ID1002">
> **[1002.写出这个数 (20)][2]**
> </a>
> 
> **题意**：给一个自然数n，n小于10^100,计算各位数字之和，按拼音输出。
> 
> **样例**：
> 
> >1234567890987654321123456789
> >
> >yi san wu
> 
> **解答**：把n的每一位相加得到sum，再根据sum的每一位，输出对应数字拼音.
>

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

>
><a id="ID1003">
>**[1003. 我要通过！(20)][3]**
></a>
>
> **题意**：给定字符串满足下面条件则答案正确输出YES，否则输出NO.
> 
>> 1. 字符串中必须仅有P, A, T这三种字符，不可以包含其它字符；
> 
>> 2. 任意形如 xPATx 的字符串都可以获得“答案正确”，其中 x 或者是空字符串，或者是仅由字母 A 组成的字符串；
> 
>> 3. 如果 aPbTc 是正确的，那么 aPbATca 也是正确的，其中 a, b, c 均或者是空字符串，或者是仅由字母 A 组成的字符串。
>
>**解答**: 根据xPATx正确，aPbTc在b=A,a=c的情况下正确
>
>而aPbTc正确，则aPbATca正确，则aPbAATcaa正确，依次aPbTc有每次b后扩展一个A则c后扩展一个a
>
>即有aPbA...ATca...a也正确（前后省略个数相同）且aPbA...ATca...a ＝ aPAA...ATaa...a
>
>以上可概括为：
>>1. *字符串中只有P、A、T*
>>
>>2. *P在前T在后,P、T仅出现一次*
>>
>>3. *P前的A个数＊PT间A的个数＝T后面A的个数；PT间A的个数至少有1个*
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

> <a id="ID1004">
> **[1004. 成绩排名 (20)][4]**
> </a>
>
>**题意**：读入n名学生的姓名、学号、成绩，分别输出成绩最高和成绩最低学生的姓名和学号
>
>**解答**：qsort排序即可。注意qsort中compare函数：
>
>>int compare(const void *a, const void *p)
>>
>>return *a - *b; // 1,2,3,4
>>
>>return *b - *a; // 4, 3, 2, 1
>>
>>也就是return值大于0则交换

```c
#include<stdio.h>
#include<stdlib.h>

typedef struct _student
{
    char name[11];
    char NO[11];
    int  score;
}Student;

int compare(const void *p, const void *q)
{
    Student *a = (Student *)p;
    Student *b = (Student *)q;
    
    return a->score - b->score;
}

int main()
{
    Student stu[1000];
    int n, i;
    
    scanf("%d", &n);
    for( i = 0; i < n; i++)
    {
        scanf("%s %s %d",stu[i].name, stu[i].NO, &stu[i].score);
    }
    
    qsort(stu,n,sizeof(stu[0]), compare);
    
    printf("%s %s\n", stu[n-1].name, stu[n-1].NO);
    printf("%s %s\n",stu[0].name, stu[0].NO);
    
    
    return 0;
}

```

>
><a id="ID1005">
>**[1005. 继续(3n+1)猜想 (25)][5]**</a>
>
>**题意：** 对于数n,按照偶数减半，奇数3*n+1减半的规则，最终会变成1。给定一个组数来判定这个规则，找出只需要判断的关键数。
>
>**解答：** 要处理的数个数不超过100个，每个数不大于100。我们可以key[n]=1先假设n是关键数，然后对每个n做猜想验证处理，遇到的中间数都标记为非关键数key[n]=0.*注意：运算中n可能大于100*，最后输出key[i]=1的i.
>
>

~~~c
#include<stdio.h>

int main()
{
    int k, i, n, c, a[101], key[101] = {0};
    scanf("%d", &k);
    
    for(i = 0; i < k; i++)
    {
        scanf("%d",&n);
        a[i] = n;
        key[n] = 1;
    }
    
    for(i = 0; i < k; i++)
    {
        n = a[i];
        if(key[n])
        {
            n = (n % 2 == 1) ? (n*3 + 1) / 2 : n / 2;
            while(n != 1)
            {
                if(n <= 100) key[n] = 0;
                n = (n % 2 == 1) ? (n*3 + 1) / 2 : n / 2;
            }
        }

    }
    
    for(n = 100, c = 0; n > 1; n--)
    	if(key[n]) c++;
    
    for(n = 100; n > 1 && c > 0; n--)
    {
        if(key[n])
        {
            printf("%d",n);
            if(--c) printf(" ");
            
        }
    }
    
    return 0;
}
~~~

><a id="ID1006"> 
> **[1006. 换个格式输出整数 (15)][6]**
></a>
>
> **题意**: 234输出BBSSS1234，23输出SS123，给定n(<1000)输出对应规定格式。
> 
> **解答**: 得到n的百、十、个位然后依照条件输出即可，十分简单
> 

~~~c
#include<stdio.h>

int main()
{
    int n, b,s,g, i;
    scanf("%d", &n);
    
    b = n / 100;
    s = (n / 10) % 10;
    g = n % 10;
    
    while( b-- ) printf("B");
    while( s-- ) printf("S");
    for(i = 1; i <= g; i++) printf("%d",i);
    
    return 0;
}
~~~

><a id="ID1007"> 
> **[1007. 素数对猜想 (20)][7]**
></a>
>
> **题意**: 现给定任意正整数N (< 105)，请计算不超过N的素数对的个数。素数对：相邻且差为2的素数对。
> 
> **解答**: n是否为素数的一般方法
>
>> 对不大于sqrt(n)的素数p做n%p，n%p=0则不为素数。一般为了提高效率会打一张素数表村p。
>>
>>有时候为了更简单：p = 3; p <= sqrt(n); p += 2。效率会相对低一些，但这题我们这样处理更简单。
>>  

~~~c
#include<stdio.h>
#include<math.h>

int isprime(int n)
{
    int i;
    for( i = 3; i <= sqrt(n); i += 2)
    {
        if( (n % i) == 0) return 0;
    }
    
    return 1;
}

int main()
{
    int n, p1, p2, count = 0;
    scanf("%d", &n);
    
    for(p1 = 3,p2 = 5; p2 <= n; p2 += 2)
    {
        if(isprime(p2))
        {
            if( p2 - p1 == 2 ) count++;    
            p1 = p2;
        }
    }
    
    printf("%d",count);
    return 0;
}


~~~


><a id="ID1008"> 
> **[1008. 数组元素循环右移问题 (20)][8]**
></a>
>
> **题意**: 数组循环右移
> 
> **解答**: 最简单的方法，另外开一个数组存放移动后的数据。
>
>>*如果需要考虑程序移动数据的次数尽量少，要如何设计移动的方法？* 
>
>刚开始有被这句话误导过，想复杂了，不过貌似到真有一个移动次数更少更节省空间的办法，暂时不管了
>
>>   

~~~c
#include<stdio.h>

int main()
{
    int i,n,m, a[100],b[100];
    scanf("%d %d", &n, &m);
    
    for(i = 0; i < n; i++)
    {
        scanf("%d",a+i);
    }
    
    for(i = 0; i < n; i++)
    {
        b[ (i + m) % n ] = a[i];
    }
    
    for(i = 0; i < n; i++)
    {
        printf("%d", b[i]);
        if(i < n-1) printf(" ");
    }   
    
    return 0;
}
~~~


><a id="ID1009"> 
> **[1009. 说反话 (20)][9]**
></a>
>
> **题意**: 单词逆序输出
> 
> **解答**:从后往前扫描，碰到空格意味着跳过了一个单词，输出，直到扫描完整个字符串。 
>
>> *注意：C语言中接受一行含有空格的字符串用gets()函数*
>> 
>> 

~~~c
#include<stdio.h>
#include<string.h>

int main()
{
    char str[81] = {0};
    gets(str);

    char *q = str + strlen(str);
    
    while(q > str)
    {
        q--;
        if(*q == ' ')
        {
            printf("%s ",q+1);
            *q = '\0';
        }
    }
    printf("%s",q);
    
    return 0;
}
~~~

><a id="ID1010"> 
> **[1010. 一元多项式求导 (25)][10]**
></a>
>
> **题意**:设计函数求一元多项式的导数。（注：xn（n为整数）的一阶导数为n*xn-1。）指数递降方式输入多项式非零项系数和指数（绝对值均为不超过1000的整数）。数字间以空格分隔。
> 
> **解答**: 容易忽略多项式为0,0的情形。
>
>>   

~~~c
#include<stdio.h>

int main()
{
    int a, n, iszero = 1;

    while(scanf("%d %d", &a,&n)!=EOF)
    {
        if(iszero && n != 0)
        {
           printf("%d %d",a*n, n-1); 
           iszero = 0;
        }
        else if( n != 0)
        {
             printf(" %d %d",a*n, n-1);
        }
    }
    
    if(iszero) printf("0 0");
    
    return 0;
}

~~~

[1]:http://www.patest.cn/contests/pat-b-practise/1001
[2]:http://www.patest.cn/contests/pat-b-practise/1002
[3]:http://www.patest.cn/contests/pat-b-practise/1003
[4]:http://www.patest.cn/contests/pat-b-practise/1004
[5]:http://www.patest.cn/contests/pat-b-practise/1005
[6]:http://www.patest.cn/contests/pat-b-practise/1006
[7]:http://www.patest.cn/contests/pat-b-practise/1007
[8]:http://www.patest.cn/contests/pat-b-practise/1008
[9]:http://www.patest.cn/contests/pat-b-practise/1009
[10]:http://www.patest.cn/contests/pat-b-practise/1010
