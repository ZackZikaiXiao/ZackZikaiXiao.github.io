---
layout:     post
title:      "分配内存malloc()与calloc()"
subtitle:   "malloc() & calloc() "
date:       2020-01-28
author:     "ZK"
tags:
    - C
---

> 最近在处理图像过程中,遇到了如何从函数中返回一个数组的问题,查阅了很多资料,最后发现了两个方法:一个是动态内存分配,第二个是返回一个结构体.这里主要是记录动态分配内存的两个函数.

1. malloc()

   C Primer Plus上的示例代码(简单修改)如下:

   ```c
   #include <stdio.h>
   #include <stdlib.h>		//包含了malloc()的库
   
   int main() {
   
       double* ptd;
       ptd = (double*)malloc(30*sizeof(double));
       ptd[0] = 1;
       printf("%f", ptd[0]);
       return 0;
   }
   ```

   运行之后输出为1,在预期之中.可以看出malloc()的函数声明如下:

   `(double*)malloc(n*sizeof(double));`

   有以下几个注意事项:

   - malloc()向系统申请分配`n*sizeof(double)`个字节的空间,返回类型为`void*`,即未确定类型的指针.C规定,void*类型可以强制转化为任何其他类型的指针,在这里通过(int\*)强制转化.
   - 函数返回后,接受的对象必须类型匹配,在此例中,都是指向`double`类型的指针.

   

2. calloc()

   对应代码如下:

   ```c
   #include <iostream>
   using namespace std;
   
   
   int main() {
   
       double* ptd;
       ptd = (double*)calloc(30, sizeof(double));
       ptd[0] = 1;
       cout<<ptd[0];
       return 0;
   }
   
   ```

   当然范围也是1.

3. free()

   这个比较简单,形参输入ptd即可.

> 即便可以动态分配内存,但貌似分配一维的,二维图片仍旧不行,有待进一步学习哦

<hr/>

> 2020-2-29补充：

> malloc(分配二维数组十分灵活，最关键的是理解二维数组指针的概念。下面提供创建5*3二维数组代码。
>
> 注意：行列数必须是常量，不可是变量。

方法一：二级指针创建

```c
    int **img = (int **)malloc(sizeof(int)*3);
    for (int i=0;i<5;i++){
        img[i] = (int*)malloc(sizeof(int)*5);
    }
```

`完整代码`

```c
#include <stdio.h>
#include <stdlib.h>
int main(){
    int **img = (int **)malloc(sizeof(int)*3);
    for (int i=0;i<5;i++){
        img[i] = (int*)malloc(sizeof(int)*5);
    }
    img[3][2] = 5;
    img[4][0] = 50;
    printf("%d\n", img[3][2]);
    printf("%d", img[4][0]);
    return 0;
}
```



方法二：指针数组创建

```c
int (*img)[3] = (int(*)[3])malloc(sizeof(int)*3*5);
```

`完整代码`

```c
#include <stdio.h>
#include <stdlib.h>
int main(){
    int (*img)[3] = (int(*)[3])malloc(sizeof(int)*3*5);

    img[3][2] = 5;
    img[4][0] = 50;
    printf("%d\n", img[3][2]);
    printf("%d", img[4][0]);
    return 0;
}
```

