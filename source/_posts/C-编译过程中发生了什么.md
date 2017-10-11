---
title: C++编译过程中发生了什么
tags:
  - Originals
number: 6
date: 2017-04-23 08:00:05
---

# 四个阶段

c++的编译过程

gcc -o hw.exe  hw.c

大致可分为四个阶段：预编译、编译、汇编、链接。

## 1. 预编译 cpp

main.cpp --> main.i

> cpp hw.c -o hw.i
> gcc -E hello.c -o hello.i

对其中的伪指令（以#开头的指令）和特殊符号进行处理。

> 1. 宏 #define
> 2. 条件编译指令 #ifdef，#ifndef，#else，#elif，#endif等
> 3. 头文件include
> 4. 特殊符号 LINE FILE

## 2. 编译和优化 cc1/as

main.i --> main.s

> cc1 hw.i -o hw.s
> gcc -S hello.i -o hello.s 

通过词法分析，语法分析，语义分析及代码优化，把预处理完的文件翻译成等价的中间代码表示或汇编代码。

编译单元：一个cpp文件和它include的头文件。当一个c或cpp文件在编译时，预处理器首先递归包含头文件，形成一个含有所有必要信息的单个源文件，这个源文件就是一个编译单元。

内部连接：如果一个名称对编译单元(.cpp)来说是局部的，在链接的时候其他的编译单元无法链接到它且不会与其它编译单元(.cpp)中的同样的名称相冲突。

外部连接：如果一个名称对编译单元(.cpp)来说不是局部的，而在链接的时候其他的编译单元可以访问它，也就是说它可以和别的编译单元交互。



## 3. 汇编 as

main.s --> main.o(依赖的其它 *.o)

> as hw.s -o hw.o
> gcc -c hello.s -o hello.o

根据汇编指令和机器指令的对照表一一翻译，将汇编代码转变成机器可以执行的命令。

编译后生成的文件，以机器码的形式包含了编译单元里的所有函数和数据、导出符号表、未解决符号表、地址重定向表等。


## 4. 链接 ld

main.o(依赖的其它 *.o) --> main可执行程序

> ld hw.o -o hw.exe
> gcc hello.o -o hello.exe

.out
linux:.so .o .a
windows:.dll .exe .obj .lib

.o 是一个最小的编译单元 
.a 就是一组 .o文件打包了
.so 除了没有 main 函数，和一个可执行程类似了。

调用链接器ld, 链接程序运行所依赖的目标文件，以及所依赖的其它库文件，最后生成可执行文件。

链接过程是将单个编译后的文件链接成一个可执行程序。前面的预编译、汇编、编译都是正对单个文件，以一个文件为一个编译单元，而链接则是将所有关联到的编译后单元文件和应用的到库文件，进行一次链接处理，之前编译过的文件 如果有用到其他文件里面定义到的函数，全局变量，在这个过程中都会进行解析。

静态链接库(.lib)和动态链接库(.dll)都是共享代码的方式。如果采用了静态链接库，则无论你愿不愿意lib中的代码指令都被直接包含进了最终生成的.exe程序中。但若是使用了动态链接库，该DLL则不会被包含进.exe程序中，当.exe程序执行的时候，再“动态”的来引用或者卸载DLL。

参考资料：

http://blog.csdn.net/edisonlg/article/details/7081357
http://www.cnblogs.com/magicsoar/p/3840682.html
http://www.cnblogs.com/dongdongweiwu/p/4743709.html
http://blog.csdn.net/yinzhuo1/article/details/47069201
http://www.cnblogs.com/litterrondo/archive/2013/01/28/2880281.html
http://www.cnblogs.com/vamei/archive/2013/04/04/2998850.html
