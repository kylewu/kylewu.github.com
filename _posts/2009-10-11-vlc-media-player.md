---
layout: post
title: 解决VLC Media Player 中文字幕乱码的问题
date: 2009-10-11 00:00:00.000000000 +02:00
published: true
categories:
- 实用软件 
tags:
- software
- ubuntu
---

![vlc]({{ site.baseurl }}/assets/3998103185_4b9b2ebd08.jpg)

重装了一次Ubuntu，带来一个问题。本来VLC Player放电影时字幕没有问题，改成GTK就可以正常显示。但是这次重装以后，仅修改encoding不起作用。搜了很多网页，主要就是修改encoding，并且把字体改为中文字体。不过最后通过Ubuntu Wiki搞定了。

方法就是进入`/etc/fonts/conf.d/`文件夹，修改`49-sansserif.conf`这个文件。将最后一个看到的字体改为一个中文字体，我改为了WenQuanYi Zen Hei。就是这么简单。Wiki的地址在[这里](http://wiki.ubuntu.org.cn/Vlc)。
