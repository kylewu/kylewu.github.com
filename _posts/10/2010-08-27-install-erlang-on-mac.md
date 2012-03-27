--- 
layout: post
title: Install Erlang on Mac
published: true
meta: 
  _edit_last: "1"
tags: 
- erlang
- mac
- OS
- Software
type: post
status: publish
---
Before install Erlang, please make sure GCC is installed.

1. Download Erlang source code from <a href="http://www.erlang.org/download.html">http://www.erlang.org/download.html</a>

2. Unarchive the file

3. run Terminal and follow the steps

cd otp_src_R14A
./configure
make
sudo make install

4. type erl in Terminal, it should be ok now.

There is a plugin for XCode to use Erlang.

Download from <a href="http://sourceforge.net/projects/quickconnect/">http://sourceforge.net/projects/quickconnect/</a> , and run it.
