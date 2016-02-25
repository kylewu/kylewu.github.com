---
layout: post
title: 为Pidgin添加Twitter支持
date: 2009-07-27 00:00:00.000000000 +02:00
published: true
categories:
- 实用软件
tags:
- gfw
- software
- twitter
---

![]({{ site.baseurl }}/assets/3761176077_9079e159ce_o.jpg "Pidgin")

最初知道Pidgin是开始使用Ubuntu，很喜欢这种IM集成的软件，可以同时登陆GTalk，MSN等主流的即时通讯。今天碰巧在网上看到Pidgin可以支持Twitter，于是搜到了这款Pidgin插件，[Microblog-Purple](http://code.google.com/p/microblog-purple/ "microblog-purple")。

[Microblog-Purple](http://code.google.com/p/microblog-purple/ "microblog-purple")是针对LibPurple开发的软件（如Pidgin，Finch）开发的插件，使用Google Code提供的SVN服务进行版本控制。

我使用的是Pidgin Portable的版本，也就是PortableApp.com开发的版本，绿色版本。这款插件也提供了针对Pidgin Portable的安装包，在Microblog-Purple主页的右方，可以找到下载链接，我所下载到的是[microblog_.0.2.2_for_pidgin_portable_2.5.x-1.exe](http://microblog-purple.googlecode.com/files/microblog_.0.2.2_for_pidgin_portable_2.5.x-1.exe "microblog-purple")。运行后选择Pidgin的安装目录即可。

[![]({{ site.baseurl }}/assets/3761977172_11e89ca745_o.png "microblog_purple")](http://farm4.static.flickr.com/3423/3761977172_11e89ca745_o.png)

[![]({{ site.baseurl }}/assets/3761977386_f97cddee9c_o.png "microblog_purple")](http://farm3.static.flickr.com/2423/3761977386_f97cddee9c_o.png)

运行Pidgin就可以在新建的窗口找到Twitter选项了，同时，插件也提供了很多设置选项，最好将Use HTTPS的勾选上。

[![]({{ site.baseurl }}/assets/3761176135_4037a6958f_o.png "Pidgin_Twitter")](http://farm4.static.flickr.com/3457/3761176135_4037a6958f_o.png)

[![]({{ site.baseurl }}/assets/3761977500_e8fbb07e40_o.png "Pidgin_Twitter")](http://farm4.static.flickr.com/3480/3761977500_e8fbb07e40_o.png)

现在Twitter被墙掉了，所以要连接上Twitter，需要简单的修改一下Host文件。在Host文件中添加如下内容

```
128.121.146.228 twitter.com
128.121.146.228 www.twitter.com
128.121.146.101 assets0.twitter.com
128.121.146.101 assets1.twitter.com
128.121.146.101 static.twitter.com
128.121.146.229 assets2.twitter.com
128.121.146.229 assets3.twitter.com
65.74.185.41 twitter.zendesk.com
65.74.185.41 help.twitter.com
```

Twitter账户设置好后，每隔60s（默认设置），就会抓取一次Twitter消息，如果有新消息，将自动弹出。 Pidgin真的是款很好的软件，市面上已经有很多类似软件了，但我感觉，Pidgin还是最好的一款。
