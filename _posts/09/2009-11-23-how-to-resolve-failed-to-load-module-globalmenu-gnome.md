--- 
layout: post
title: "\xE5\xA6\x82\xE4\xBD\x95\xE8\xA7\xA3\xE5\x86\xB3Failed to load module \"globalmenu-gnome\""
published: true
meta: {}

tags: 
- Linux
- Software
- Ubuntu
type: post
status: publish
---
<img class="alignnone" src="http://farm3.static.flickr.com/2759/4125268091_88e3b40a34_s.jpg" alt="globalmenu" width="75" height="75" />Global Menu是Mac OS系统的一个基本功能，用过Mac的肯定都知道。使用Gnome的Linux一样可以做到，<a href="http://code.google.com/p/gnome2-globalmenu/">这里</a>是gnome2-globalmenu的项目主页，有兴趣的可以看一下，里面的wiki挺全，有安装方法介绍。这篇文章不是介绍如何安装global menu，而是解决卸载后出现的一个小问题。

在卸载global menu后，如果你从命令行启动程序，就会发现往往都会提示如下的错误
<blockquote>Gtk-Message: Failed to load module "globalmenu-gnome": libglobalmenu-gnome.so: cannot open shared object file: No such file or directory</blockquote>
说明在启动程序时，依然去调用globalmenu-gnome模块，但是由于已经卸载，所以提示没有找到。

解决方法很简单，运行gconf-editor，然后找到app -> gnome_setting_daemon -> gtk-modules，在右方可以看到global menu还是选中状态，取消选中或者删除就可以了。这样子再次运行程序就不会出现错误了。
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 0px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">gconf-editorg</div>
