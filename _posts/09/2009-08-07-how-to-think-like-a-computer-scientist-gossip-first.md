--- 
layout: post
title: "How to Think Like a Computer Scientist \xE5\xAD\xA6\xE4\xB9\xA0\xE7\xAC\x94\xE8\xAE\xB0(\xE4\xB8\x80)"
published: true
meta: {}

tags: 
- Coding
- gossip
- tutorial
type: post
status: publish
---
<a class="tt-flickr tt-flickr-Square" title="gasp_lessons" href="http://www.flickr.com/photos/kylewu/3798515670/"><img class="alignnone" src="http://farm4.static.flickr.com/3447/3798515670_4ac9f30808_s.jpg" alt="gasp_lessons" width="1" height="1" /></a> <a title="How to Think Like a Computer Scientist: Learning with Python v2nd Edition" href="http://openbookproject.net//thinkCSpy/index.html" target="_blank">How to think like a computer scientist : Learning with Python v2nd edition</a>

很不错的一个教程，不仅仅从头讲解了Python，更重要的是帮助我把计算机编程知识进行了一次梳理。

学习笔记（一）针对的是第一章 <a title="The way of the program" href="http://openbookproject.net//thinkCSpy/ch01.html#the-first-program" target="_blank">The way of the program</a>

作为一名计算机科学家，最重要的是解决问题的能力。(<strong>Problem solving</strong>)
<h4>Python</h4>
编程语言可以分为高层语言(<strong>High-level language</strong>)和低层语言(<strong>Low-level language</strong>)。高层语言，比如c++，java，python，需要先转换成低层语言，比如汇编，因此会花费一些时间，这也是高层语言的缺陷。但是高层语言有很大优势
<ol>
	<li>编程方便，容易理解</li>
	<li>更加轻便(<strong>portable</strong>)，可移植性更好，底层语言需要针对不同平台进行修改</li>
</ol>
高层语言转换为地层语言的程序有两种：解释器(<strong>interpreter</strong>)和编译器(<strong>compiler</strong>)。解释器读取代码，一步步执行代码。编译器把源代码 (<strong>Source cod</strong>e)编译为对象码(<strong>Object code</strong>)，然后再执行。

现代的编程语言普遍采用了这两种方式，先把源代码编译为字节码(<strong>Byte code</strong>)，然后在虚拟机(<strong>Virtual machine</strong>)中解释执行。

Python也采用了这两种方式，但是由于程序员编程的方式，一般把python看做解释性语言。Python有两种解释方式：<strong>shell mode</strong>和<strong>script mode</strong>。
<h4>什么是程序</h4>
程序是顺序的计算指令。它包含了input, output, math, conditional execution, repetition，任何程序都是由这几个要素组成的。
<h4>什么是Debug</h4>
程序的错误就是<strong>bug</strong>，解决bug就是<strong>debug</strong>。

程序的错误分为三种：语法错误(<strong>syntax error</strong>)，运行时错误(<strong>runtime error</strong>)，语意错误(<strong>semantic error</strong>)。

对于一些人，编程和debug是同时进行的，可以保证程序的可运行性。
<h4>形式语言和自然语言</h4>
自然语言(<strong>Natural language</strong>)就是世界上的语言，英语法语等
形式语言(<strong>Formal language</strong>)是人们为了某个目的设计的，比如数学和化学中语言

形式语言有两个要素：<strong>token</strong>和<strong>structure</strong>。分析语言的过程就是<strong>parsing</strong>。

相比于形式语言，自然语言不明确(ambiguity),重复(redundancy)，literalness。
