---
layout: post
title: Several useful linux commands
date: 2011-03-19 00:00:00.000000000 +01:00
published: true
categories:
- 杂七杂八
tags:
- linux
- os
---
* `$ sudo !!` - run the previous command with superuser privileges.
* `$ cd !$` - the "!$" is a shortcut for the argument used in the last command. So if you create a directory in one like using mkdir, you can type this command to change to that directory without needing to type out the whole directory name. Handy!
* `$ !cd` - re-run the most recent command starting with "cd".
* `$ ^save^dave^` - re-run the previous command, replacing the first instance of "save" with "dave".
* `$ CTRL-r` - search backwards through your commands (great for re-running a recent command).
