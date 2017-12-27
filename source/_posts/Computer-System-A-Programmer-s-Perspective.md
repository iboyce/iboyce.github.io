---
title: 'Computer System, A Programmer''s Perspective'
date: 2017-08-21 14:22:46
tags:
      - 系统结构
      - 经典著作
categories: 深耕码农
mathjax: true
---


# 导言
1. 信息就是位+上下文，如文本文件、二进制文件；
2. 程序：文本——预处理器——编译器——汇编器——链接器——可执行文件
  ![CS_compile](http://p15i7i801.bkt.clouddn.com/d8403afcfd487487262309d0137d406f.png)

从JAVA的角度上看，JAVACODE在JVM上亦符合上述过程。
JVM这个代码级机器可参考百度百科，包括对JVM指令系统、寄存器、栈结构及子系统（GC、类加载器）等
![JVM](http://p15i7i801.bkt.clouddn.com/8c5d39071eb21c9f569e9e46119377d3.png)
![cs_jvm_stack](http://p15i7i801.bkt.clouddn.com/32f2e3db6434701a8206f6ce128bf139.png)

**基本上，一个线程启动后分配一个栈（-XSSS），保存局部变量、操作数、指向常量池的引用及返回地址，这些称为一个桢，进入新方法后，再压入一个帧；同时分配一个私有PC寄存器用于任何分支，循环，方法调用，判断，异常处理，线程等待以及恢复线程，递归等等； 所有的线程共享方法区（PERM)及堆**
