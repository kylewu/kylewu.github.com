---
layout: post
title: Install Erlang on Mac
date: 2010-08-27 00:00:00.000000000 +02:00
published: true
categories:
- 编程技术
tags:
- erlang
- mac
- os
- software
---

Before install Erlang, please make sure GCC is installed.

* Download Erlang source code from [http://www.erlang.org/download.html](http://www.erlang.org/download.html)
* Unarchive the file
* run Terminal and follow the steps

```shell
    cd otp_src_R14A
    ./configure
    make
    sudo make install
```

* type erl in Terminal, it should be ok now.

There is a plugin for XCode to use Erlang.

Download from [http://sourceforge.net/projects/quickconnect/](http://sourceforge.net/projects/quickconnect/) , and run it.
