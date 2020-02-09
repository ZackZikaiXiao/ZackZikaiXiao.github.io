---
layout:		post
title:		"GCC常用语法"
subtitle:	"Frequently-used command in GCC"
date:		2020-02-09
author:		"Zack"
tags:	
    - C		
---
# 一、GCC

## 1.编译一步到位： 

` gcc test.c -o test`

## 2.完整过程

1. 预处理

`gcc -E test.c -o test.i`

2. 编译为汇编代码

`gcc -S test.i -o test.s`

3. 汇编目标文件

`gcc -c test.s -o test.o`

4. 链接

` gcc test.o -o test`

## 3.多文件编译

`gcc -c test1.c test2.c -o test`



# 二、GDB

## 1.启动调试

`gdb filename`

## 2.断点

- 查看断点

`info breakpoints`

- 根据行号设置断点

` b num`

- 根据函数名设置断点

` b function`

-  根据条件设置断点

`break test.c:23 if b==0`

`condition 1 b==0`

- 启动禁用与清除

` enable bnum`

`able bnum`

`clear bnum`

## 3.变量查看

- 普通变量查看

`p var`

- 打印指针指向内容

`p *pointer`

## 4. 自动显示变量内容

> 用法与print一样

`display var`

## 5.调试

- 单步执行

`n`ext

- 单步进入

`s`tep

- 继续执行到下一个断点

` c`ontinue

- 继续执行到指定位置until(第29行)

`u 29`

- 跳过执行

> 可以在step时跳过一些不想关注的函数

`skep function add`

## 6.源码查看

- 列出源码

`l`ist

后可`+`或`-`

- 列出指定行附近源码(第9行)

`l 9`

- 列出制定函数附近源码

`l function`

## 7.编辑源码

```bash
EDITOR=/usr/bin/vim
export EDITOR	

edit 3 			#编辑第三行
edit add 		#编辑add函数
edit test.c:5	#编辑test.c的第5行

shell gcc -g -o main main.c test.c #重新编译
```
