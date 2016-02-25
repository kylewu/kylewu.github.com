---
layout: post
title: 通过U盘安装Gentoo
date: 2009-05-21 00:00:00.000000000 +02:00
published: true
categories:
- 操作系统
tags:
- linux
- os
---

刚刚将毕业答辩的ppt完成初稿，突然想试一下通过U盘安装Gentoo，所以尝试了一下

在Gentoo的官网上下载minimal的[iso](http://gentoo.ussg.indiana.edu//releases/x86/2008.0/installcd/install-x86-minimal-2008.0.iso "download gentoo")文件。

下载UltraISO。我使用的是9.1.2版本，链接就不写了，同学们自己搜一下。将U盘插入，启动UltraISO，菜单选择“启动光盘” --> “写入硬盘映像”。

![]({{ site.baseurl }}/assets/3549448085_2a07270d8d_o.png "UltroISO")

格式化后，写入U盘

![]({{ site.baseurl }}/assets/3549448091_a347beecc1_o.png "UltraISO")

重启时，进入BIOS，调整启动顺序，我这里需要把硬盘改为我的U盘，有些机器似乎可以直接选择移动设备。这时就应该可以从U盘启动了。现在大容量U盘比比皆是，而且价格便宜，以后面对iso文件不用再刻盘安装了，也不用麻烦的硬盘安装了，直接通过U盘就可以了。

P.S. 别忘了把U盘内的资料备份，否则资料丢失可就得不偿失了。
