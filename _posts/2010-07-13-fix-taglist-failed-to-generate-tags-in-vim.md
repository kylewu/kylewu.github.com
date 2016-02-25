---
layout: post
title: 'Fix ''Taglist: Failed to generate tags'' in Vim'
date: 2010-07-13 00:00:00.000000000 +02:00
published: true
categories:
- 编程技术
tags:
- software
- vim
---

When open taglist in vim, it may says:

> Taglist: Failed to generate tags for /my/path/to/file
>
> ctags: illegal option -- -^@usage: ctags [-BFadtuwvx] [-f tagsfile] file ...

Solution is quite easy, open .vimrc and add the following line

`let Tlist_Ctags_Cmd='/location/ctags'`

In my mbp, Snow Leopard, it is `/opt/local/var/macports/software/ctags/5.8_0/opt/local/bin/ctags`
