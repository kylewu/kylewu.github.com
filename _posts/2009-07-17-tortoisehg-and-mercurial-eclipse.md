---
layout: post
title: TortoiseHg and Mercurial Eclipse
date: 2009-07-17 00:00:00.000000000 +02:00
published: true
categories:
- 实用软件
tags:
- cvs
- eclipse
- google
- mercurial
- software
- svn
---

近期在做一个小项目，使用Google Code存储代码，这才发现Google Code 已经支持Mercurial了。于是赶紧把Mercurial装入了机器，并安装了Eclipse的插件，下面简要介绍一下过程。

用过cvs和svn的同学们肯定了解这个小乌龟，不过针对Mercurial的版本TortoiseHg的小乌龟在后背上多了Hg两个字母。

[![]({{ site.baseurl }}/assets/3726156014_ec9b032f86_o.png "TortoiseHg")](http://farm3.static.flickr.com/2548/3726156014_ec9b032f86_o.png)

这里是TortoiseHg的[下载网页](http://bitbucket.org/tortoisehg/stable/downloads/ "TortoiseHg")。选择所用系统的响应版本即可。安装过程与TortoiseSVN大概相同，装好后重新启动就可以了。在右键菜单中多了TortoiseHg的一个菜单项。

与SVN和CVS相比，由于是分布式概念的版本控制系统，所以使用上与他们不完全一样。至于有何不同，可以参考我之前的两篇转帖。

至此，TortoiseHg安装完毕，有repo的同学们可是尝试使用一下。

[Mercurial Eclipse](http://www.vectrace.com/mercurialeclipse/ "Mercurial Eclipse")是一款Eclipse插件，它使Eclipse拥有了对Mercurial的支持。安装可以根据自己喜好，是自定义文件夹还是直接Software Updates(这个的地址是http://www.vectrace.com/eclipse-update/) Eclipse一个工程上右键选Team，然后选Share Project，弹出如下的对话框，然后下一步，选择工程文件夹，完成就可以了。

[![]({{ site.baseurl }}/assets/3725349343_16ec59804e_o.png "MercurialEclipse")](http://farm3.static.flickr.com/2539/3725349343_16ec59804e_o.png)

再次右键选Team就可以看见这样的菜单了，包含了各种Mercurial的操作。

[![]({{ site.baseurl }}/assets/3725349385_92ab6f83b9_o.png "MercurialEclipse")](http://farm3.static.flickr.com/2523/3725349385_92ab6f83b9_o.png)

这里没有介绍Mercurial的用法，其实对于版本控制的概念有所了解，那么使用也就是很简单的事情了。
