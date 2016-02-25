---
layout: post
title: "DUbuntu Jaunty Ctrl+Alt+Backspace"
date: 2009-06-04 00:00:00.000000000 +02:00
published: true
categories:
- 操作系统
tags:
- os
---

很多同学应该已经习惯了Ctrl+Alt+Backspace来重启X桌面。但是在Ubuntu Jaunty中，这个快捷键不起作用了。Ubuntu此举是为了避免用户误操作。从我个人来讲，没有了Ctrl+Alt+Backspace十分不方便。

恢复快捷键很方便：

安装dontzap

    sudo apt-get dontzap

Disable dontzap

    sudo dontzap --disable

重启电脑。

好了，你可以使用Ctrl+Alt+Backspace了。
