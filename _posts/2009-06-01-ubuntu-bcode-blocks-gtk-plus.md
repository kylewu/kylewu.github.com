---
layout: post
title: Ubuntu下Code----Blocks的GTK+设置
date: 2009-06-01 00:00:00.000000000 +02:00
published: true
categories:
- 实用软件
tags:
- software
- ubuntu
---

在Windows下，Code::Blocks的设置很简单，找到GTK+所在的文件夹，将include,lib文件夹分别写入就可以了。但是在Ubuntu下没有一个单独的文件夹保存所有这些文件，所以配置要麻烦一些。

不过使用pkg-config就很简单了。pkg-config可以帮助我们找到include和lib路径。

命令行下直接键入：

    pkg-config --cflags gtk+-2.0
    pkg-config --libs gtk+-2.0

可以看一下效果。打开Code::Blocks，在Global variable选项里，将include和lib中分别填入如下配置：

    pkg-config --cflags gtk+-2.0
    pkg-config --libs gtk+-2.0

![]({{ site.baseurl }}/assets/3583949494_4192c8f8f2_o.png "Code::Blocks")

这样就可以了，写一个示例程序直接跑就可以了，不会再报找不到头文件的错误了。

![]({{ site.baseurl }}/assets/3583141723_1b13c89451_o.png "GTK+")

这里补充几个可能用到的内容

    sudo apt-get install build-essential #这将安装gcc/g++/gdb/make等基本编程工具
    sudo apt-get install gnome-core-devel #这将安装 libgtk2.0-dev libglib2.0-dev 等开发相关的库文件
    sudo apt-get install pkg-config #用于在编译GTK程序时自动找出头文件及库文件位置
    sudo apt-get install devhelp #这将安装 devhelp GTK文档查看程序
    sudo apt-get install libglib2.0-doc libgtk2.0-doc #这将安装 gtk/glib 的API参考手册及其它帮助文档
    sudo apt-get instal glade libglade2-dev #这将安装基于GTK的界面构造程序
