---
layout: post
title: How to Think Like a Computer Scientist
date: 2009-08-07 00:00:00.000000000 +02:00
published: true
categories:
- 编程技术
tags:
- gossip
- tutorial
---

![gasp_lessons]({{ site.baseurl }}/assets/3798515670_4ac9f30808_s.jpg)

[How to think like a computer scientist : Learning with Python v2nd edition](http://openbookproject.net//thinkCSpy/index.html "How to Think Like a Computer Scientist: Learning with Python v2nd Edition")很不错的一个教程，不仅仅从头讲解了Python，更重要的是帮助我把计算机编程知识进行了一次梳理。

学习笔记（一）针对的是第一章 [The way of the program](http://openbookproject.net//thinkCSpy/ch01.html#the-first-program "The way of the program")

作为一名计算机科学家，最重要的是解决问题的能力。(**Problem solving**)

#### Python

编程语言可以分为高层语言(**High-level language**)和低层语言(**Low-level language**)。高层语言，比如c++，java，python，需要先转换成低层语言，比如汇编，因此会花费一些时间，这也是高层语言的缺陷。但是高层语言有很大优势

1.  编程方便，容易理解
2.  更加轻便(**portable**)，可移植性更好，底层语言需要针对不同平台进行修改

高层语言转换为地层语言的程序有两种：解释器(**interpreter**)和编译器(**compiler**)。解释器读取代码，一步步执行代码。编译器把源代码 (**Source cod**e)编译为对象码(**Object code**)，然后再执行。\n 现代的编程语言普遍采用了这两种方式，先把源代码编译为字节码(**Byte code**)，然后在虚拟机(**Virtual machine**)中解释执行。

Python也采用了这两种方式，但是由于程序员编程的方式，一般把python看做解释性语言。Python有两种解释方式：**shell mode**和**script mode**。


#### 什么是程序

程序是顺序的计算指令。它包含了input, output, math, conditional execution, repetition，任何程序都是由这几个要素组成的。

#### 什么是Debug

程序的错误就是**bug**，解决bug就是**debug**。

程序的错误分为三种：语法错误(**syntax error**)，运行时错误(**runtime error**)，语意错误(**semantic error**)。

对于一些人，编程和debug是同时进行的，可以保证程序的可运行性。

#### 形式语言和自然语言

自然语言(**Natural language**)就是世界上的语言，英语法语等

形式语言(**Formal language**)是人们为了某个目的设计的，比如数学和化学中语言

形式语言有两个要素：**token**和**structure**。分析语言的过程就是**parsing**。

相比于形式语言，自然语言不明确(ambiguity),重复(redundancy)，literalness。
