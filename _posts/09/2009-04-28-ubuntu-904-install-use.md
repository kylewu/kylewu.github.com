--- 
layout: post
title: !binary |
  VWJ1bnR1IDkuMDTlronoo4Xor5XnlKg=

published: true
meta: {}

tags: 
- OS
- Ubuntu
type: post
status: publish
---
Ubuntu 9.04在大家的期待中隆重release，还没下载的同学快去Ubuntu的网站<a title="Ubuntu" href="http://www.ubuntu.com/getubuntu/download" target="_blank">下载</a>一个安装镜像吧。

与Ubuntu 8.10 一样，在9.04版中自带了wubi，这样，使用windows的同学可以直接在windows中安装Ubuntu了。稍微介绍一下windows下安装ubuntu的方法：
用一个虚拟光驱载入安装的iso，然后在根目录下找到wubi.exe，双击之。然后稍微填入几个安装的相关参数，比如硬盘大小，系统密码等，很简单的。最后确定重启即可。Ubuntu会自动安装的。

Ubuntu的启动画面不会截取，这里就不贴图了，感觉比前几个版本要好看很多。填入用户名和密码，登录。感觉有以下几点变化：

<!--more-->

1. 桌面背景又更新了，感觉还不错。
2. 对中文的支持有了很大进步，当然，想要完全的中文菜单还是要更新语言支持。
3. 如果使用中文安装Ubuntu，那么home下的默认文件夹是中文，其实我不是很喜欢这种设置，在控制台下操作不是很方便。8.10已经是这样了，看来Ubuntu还是希望这样的设置能够多吸引新的用户。

<img class="alignnone" title="Home Folder" src="http://farm4.static.flickr.com/3622/3483016078_56e020a9c1_o.png" alt="" width="557" height="233" />

4. 细心的用户会发现，在系统菜单，系统管理中有一个小工具Computer Janitor，这个小工具能够帮助你清理一些安装包，还是挺实用的。

<img class="alignnone" title="Janitor" src="http://farm4.static.flickr.com/3345/3483016084_c9d38b56c7_o.png" alt="" width="546" height="666" />

接下来让我们装一些软件。首先要改一下sourcelist，我使用的是163的源。
<blockquote>网易163更新服务器：

deb http://mirrors.163.com/Ubuntu/ jaunty main restricted universe multiverse
deb http://mirrors.163.com/Ubuntu/ jaunty-security main restricted universe multiverse
deb http://mirrors.163.com/Ubuntu/ jaunty-updates main restricted universe multiverse
deb http://mirrors.163.com/Ubuntu/ jaunty-proposed main restricted universe multiverse
deb http://mirrors.163.com/Ubuntu/ jaunty-backports main restricted universe multiverse
deb-src http://mirrors.163.com/Ubuntu/ jaunty main restricted universe multiverse
deb-src http://mirrors.163.com/Ubuntu/ jaunty-security main restricted universe multiverse
deb-src http://mirrors.163.com/Ubuntu/ jaunty-updates main restricted universe multiverse
deb-src http://mirrors.163.com/Ubuntu/ jaunty-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/Ubuntu/ jaunty-backports main restricted universe multiverse</blockquote>
apt-get update后，安装一下常用软件。

QQ可以正常的安装和使用。但是LibFetion不行，点击后没有反应，十分需要飞信的朋友可以去下载<a title="LibFetion" href="http://www.libfetion.cn/Linux_demoapp_download.html" target="_blank">源代码</a>，自己编译一下，方法见<a title="LibFetion" href="http://www.libfetion.cn/Docs-dve%5CBuild-LibFx-on-ubuntu.txt" target="_blank">这里</a>。有图有真相，上图两张。

<img class="alignnone" title="Linux QQ" src="http://farm4.static.flickr.com/3374/3483016070_a8b4bf1dc0_o.png" alt="" width="305" height="546" /><img class="alignnone" title="Linux Fetion" src="http://farm4.static.flickr.com/3313/3483018422_968d5b0f17_o.png" alt="" width="286" height="525" />

我又装了一个Geany，一个很不错的ide，有兴趣的同学可以玩一玩。

<img class="alignnone" title="Geany" src="http://farm4.static.flickr.com/3409/3483016076_2a37fb9284_m.jpg" alt="" width="240" height="142" />

当然还要看看我的博客嘛

<img class="alignnone" title="Ubuntu Kylewu" src="http://farm4.static.flickr.com/3597/3483016096_6f6bdf2fb8_b.jpg" alt="" width="1024" height="640" />

哈哈，是的，我安装了Compiz来感受一下令人晕眩的桌面。如何安装Compiz不是今天的主题，不过希望这样能够吸引更多的同学加入Ubuntu。
