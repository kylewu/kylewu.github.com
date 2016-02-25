---
layout: post
title: Gaia Dev Env
date: 2012-05-09 00:00:00.000000000 +02:00
type: post
published: true
status: publish
categories:
- 编程技术
tags:
- b2g
- gaia
---

Vagrant
=====

Personally, I prefer working with [Vagrant](http://vagrantup.com/). Thanks to @rhelmer, here is his repo [b2g-vagrant](https://github.com/rhelmer/b2g-vagrant/). It contains a vagrant configure file and puppet file. The README file is quite comprehensive, but please notice, it will download a box file over 10G when you run `vagrant up` the first time.

SSH directly to VM
=====

Vagrant provides a clean way to develop, however, it is not convenient to connect to VM. I have to go to the vagrant folder and `vagrant ssh`.

[vagrant-proxyssh](https://github.com/kvs/vagrant-proxyssh) is a hack to use `ssh` directly from command line. If you do not like to install it, copy and paste the following words into your `~/.ssh/config`

<script src="https://gist.github.com/kylewu/2641244.js"></script>

SSHFS
=====

Now, I can use `ssh vagrant` to connect to VM directly. I also would like to mount remote folder to local machine using [sshfs](http://fuse.sourceforge.net/sshfs.html).

The command is quite simple:
`*sshfs vagrant:/home/vagrant/src/B2G/gaia ~/gaia -oauto_cache,reconnect,defer_permissions,negative_vncache,volname=gaia*`

Host Gaia in Apache
=====

Next, let us see how to host gaia in Apache (All the code in this part comes from [gaia-hacking](https://wiki.mozilla.org/Gaia/Hacking), I just make it short)

Install apache2 in VM
=====

`sudo apt-get install apache2`

Create host config file `/etc/apache2/sites-available/gaiamobile.org`

<script src="https://gist.github.com/kylewu/2641287.js"></script>

Run the following commands in order

    sudo a2enmod expires
    sudo a2enmod vhost_alias
    sudo a2ensite gaiamobile.org
    sudo apache2ctl graceful

We need to modify Vagrant configure file to visit apache from local machine. Add the next line in Vagrant configure file

    config.vm.forward_port 80, 4567

And run `vagrant reload`. Then we can visit 127.0.0.1:4567.

To see real gaia interface, add following lines in `/etc/hosts`, and open `homescreen.gaiamobile.org`

    127.0.0.1     gaiamobile.org
    127.0.0.1     homescreen.gaiamobile.org
    127.0.0.1     dialer.gaiamobile.org
    127.0.0.1     sms.gaiamobile.org
    127.0.0.1     browser.gaiamobile.org
    127.0.0.1     maps.gaiamobile.org
    127.0.0.1     camera.gaiamobile.org
    127.0.0.1     gallery.gaiamobile.org
    127.0.0.1     video.gaiamobile.org
    127.0.0.1     market.gaiamobile.org
    127.0.0.1     music.gaiamobile.org
    127.0.0.1     settings.gaiamobile.org
    127.0.0.1     clock.gaiamobile.org
    127.0.0.1     crystalskull.gaiamobile.org
    127.0.0.1     penguinpop.gaiamobile.org
    127.0.0.1     towerjelly.gaiamobile.org
    127.0.0.1     wikipedia.gaiamobile.org
    127.0.0.1     cnn.gaiamobile.org
    127.0.0.1     bbc.gaiamobile.org
    127.0.0.1     nytimes.gaiamobile.org
    127.0.0.1     calculator.gaiamobile.org
    127.0.0.1     system.gaiamobile.org

For more detail about hacking Gaia, please go to [gaia-hacking](https://wiki.mozilla.org/Gaia/Hacking).

Mac-B2G-Desktop
======

If you are a lazy man like me and you are using Mac, maybe you like to have a working B2G browser. @pauljt provides a build of b2g desktop for Mac OS in [mac-b2g-desktop](https://github.com/pauljt/mac-b2g-desktop).

Gaia
=====

All previous work is to prepare the dev env. It is time to meet Gaia.

Go to Gaia folder and modify Makefile. Set `DEBUG` to 1 and `Port` to 4567. Then run `make`. It will do a lot of work and what we need is the profile it generates.

That's all. Open your browser with the profile we just get
`/Applications/B2G.app/Contents/MacOS/b2g -profile ~/gaia/profile`

We will get the window just like the image in the beginning in this post.
