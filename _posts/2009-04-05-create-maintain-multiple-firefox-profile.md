---
layout: post
title: 创建和管理多个Firefox Profile
date: 2009-04-05 00:00:00.000000000 +02:00
published: true
categories:
- 互联网
tags:
- firefox
- software
---

What is Firefox Profile?
=====

Mozilla的官方定义:

> Any changes you make while using Firefox are stored in files so that they can be used the next time you run Firefox. These changes can be obvious, like your home page, or changes you've made to the toolbar, but also include things like your history, what sites you've visited, and text you've entered into forms like search fields. They're all stored in the same location, called a profile folder.
>
> These files are kept separately from the program files that Firefox uses to run, which don't change. This means that you can uninstall Firefox without losing your settings, and that if something goes wrong with an update your information will still be there. It also means you don't have to reinstall Firefox in order to clear your information, or troubleshoot a problem.

意思就是说，profile是一组Firefox为你建立的文件，其中包含了你的个人信息，比如书签，密码等。profile没有放在Firefox的安装目录，即使你卸载Firefox，你的信息都不会丢失的，当然，如果想清除你的信息，也不需要重新安装Firefox，只需要把profile删除就可以了。

Why need Firefox Profile?
=====

比如我作为一名大学生，在宿舍中生活，有时就可能和室友共享一台电脑，有些信息是不想和别人分享的(密码，历史记录之类的)。又或者是我们自己有一些特殊的原因，比如工作，游戏需要不同的Firefox设置。碰到这些情况，通过配置不同的profile，让我们启动Firefox后进入不同的环境。使用profile保证了私密性，也让Firefox更加简洁，专注某一项任务。同时，将不同用途的插件分开也有利于Firefox的启动和使用速度。

How to use Firefox Profile?
=====

正常情况下，我们启动Firefox时采用默认的profile(default)。Firefox's profile manager能够帮助我们管理Firefox Profile。为了启动Firefox profile manager，需要从命令行启动。简单一点可以从开始--运行启动，在运行中键入`firefox.exe --profilemanager`。就像这样：

![]({{ site.baseurl }}/assets/3413018171_18c37eb96a_o.png)

这样我们会看到Firefox's profile manager。可以创建，重命名，删除profile文件。

![]({{ site.baseurl }}/assets/3413018139_b7832edb53_o.png)

注意“启动时不询问”选项，不选中的话，每次启动Firefox都将弹出这个窗口让你选择profile。

看到这里，我们就该看看如何利用profile帮助我们管理Firefox了。
桌面上找到Firefox的快捷方式，在末尾加上`-P profilename`：

![]({{ site.baseurl }}/assets/3413813910_7bfe75a527_o.png)

这是我专门为开发Firefox插件建立的profile。

先写到这里，明天会有关于如何备份profile的介绍。
