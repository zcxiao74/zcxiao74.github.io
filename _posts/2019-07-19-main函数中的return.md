---
layout: post
title: "main函数"
date: 2019-07-19 
tags: C语言  
---

# main函数

```
#include <stdio.h>

int main(int argv,char* argc[])
{
        printf("hello world\n");
        printf("atgv is %d \n",argv);
        int i;
        for (i=0;i<argv;i++){
        	printf("argc[%d] is %s",i,argc[i]);
        }
        return 0;
}
```



## main函数中的return

连续执行两条指令：`$ gcc main.c -o main.out && ./main.out`(第一条成功后才会返回第二条)

判断执行成功：`echo $?`	->	返回错误码(即return  0)，0代表成功



## main函数中的参数

`./m2.out`	->	argv is 1

`./m2.out -l`	->	argv is 2

`./m2.out -l -a`	->	argv is 3

argv	->	程序共有几个参数

argc[]	->	程序中的参数组成的列表

