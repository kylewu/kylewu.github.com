---
layout: post
title: 将Ubuntu美化为Mac
date: 2009-09-27 00:00:00.000000000 +02:00
published: true
categories:
- 操作系统
tags:
- os
- software
- ubuntu
---

![Screenshot-awn_elements.png]({{ site.baseurl }}/assets/3957540769_49b215598d.jpg)

很早以前就听说过Mac4Lin这个美化包，今天尝试了一下，效果很不错，先上张图同学们看看效果。

![Mac4Lin Screenshot]({{ site.baseurl }}/assets/3957547363_62fd364490.jpg "Mac4Win")

ok，感觉还是不错的吧，下面介绍一下如何安装。

从Mac4Lin的[主页](http://sourceforge.net/projects/mac4lin/ "Mac4Lin")上下载到最新的包，我下载的还是1.0，32.9MB。下载好后解压，然后cd到解压目录，执行
`sh Mac4Lin_Install_v1.0.sh`。安装过程中会有提示，请按照提示操作。

安装完以后就很明显看到效果了。希望使用Dock的同学可以再安装AWN Dock。

    sudo apt-get install avant-window-navigator

![Mac4lin dock]({{ site.baseurl }}/assets/3957540769_49b215598d.jpg "Mac4Win Dock")

我很想在Dock上添加RTM的item，Google上搜索了一下，AWN Dock有这个applet，但是默认的包没有包含，需要再安装extra包。

    sudo apt-get install awn-applets-python-extras

然后，为了运行RTM的applet，还需要有gtkmozembed的python module，没有的同学执行下面的命令。

    sudo apt-get install python-gnome2-extras-dev

这样RTM applet就可以使用了。

![Mac4lin rtm]({{ site.baseurl }}/assets/3958316400_f9ceab61e5.jpg "Mac4Win RTM")

这里不多说细节的美化了，想进一步的同学请移步[这里](http://maketecheasier.com/turn-your-ubuntu-hardy-to-mac-osx-leopard/2008/07/23)。
