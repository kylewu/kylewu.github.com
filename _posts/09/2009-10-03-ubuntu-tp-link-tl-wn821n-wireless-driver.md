--- 
layout: post
title: !binary |
  5oiQ5YqfVWJ1bnR15LiL5a6J6KOFVFAtTGluayBUTC1XTjgyMU7ml6Dnur/n
  vZHljaHnmoTpqbHliqg=

published: true
meta: {}

tags: 
- Linux
- OS
- Ubuntu
type: post
status: publish
---
我的笔记本没有无线网卡，出国前特意买了一个无线网卡，以备不时之需。我买的无线网卡是TP-Link TL-WN821N，只有Windows的驱动，不支持Linux。今天搜索了一下，找到了解决方案。

其实方法十分简单：
1.安装ndiswrapper，尝试apt-cache search搜索一下，我9.04Ubuntu可以找到，Sweden的源。
接下来就可以找到System -> Administration -> Windows Wireless Drivers。
2.这时候需要无线网卡的驱动，从<a href="http://www.iogear.com/support/driver/GWU623.zip">这里</a>下载。
然后Install这个驱动。
3.安装wicd，我可以从源中直接安装，找不到的同学自己搜索一下官网吧。
安装以后重启一下，就可以发现wicd network manager已经代替了原来的Network Manager。

还是很简单的，这个方法我只测试了我自己的TP-Link TL-WN821N无线网卡，不知道其他TP-Link的可不可行。
最后提供两个网址，我也是从这里找到解决办法的，<a href="http://forum.ubuntu.org.cn/viewtopic.php?f=116&t=147947">Link1</a>，<a href="http://www.paoto.com/2009/08/11/ubuntu-904-%E6%97%A0%E7%BA%BF%E7%BD%91%E5%8D%A1%E4%B8%8D%E8%83%BD%E6%AD%A3%E7%A1%AE%E4%BD%BF%E7%94%A8%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88/">Link2</a>。
