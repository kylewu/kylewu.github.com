---
layout: post
title: "Gaia Dev Env"
description: ""
category: b2g
tags: [b2g, gaia]
---
{% include JB/setup %}

Vagrant
==========

Personally, I prefer working with [Vagrant]. Thanks to
@rhelmer, here is his repo [b2g-vagrant]. It contains a vagrant configure file and
puppet file. The README file is quite comprehensive, but please notice, it will
download a box file over 10G when you run *vagrant up* the first time.

SSH directly to VM
==========

Vagrant provides a clean way to develop, however, it is not convenient to
connect to VM. I have to go to the vagrant folder and *vagrant ssh*.
[vagrant-proxyssh] is a hack to use *ssh* directly from cml. If you do not like
to install it, copy and paste the following words into your *~/.ssh/config*

<script src="https://gist.github.com/2641244.js"> </script>

SSHFS
======

Now, I can use *ssh vagrant* to connect to VM directly. I also would like to mount
remote folder to local machine using [sshfs]. 
The command is quite simple:

	*sshfs vagrant:/home/vagrant/src/B2G/gaia ~/gaia -oauto_cache,reconnect,defer_permissions,negative_vncache,volname=gaia*

Host Gaia in Apache 
===========

In the end, let us see how to host gaia in Apache (All the folling part comes from
[gaia-hacking], I just make it short)

Connect to VM first and install apache2

	sudo apt-get install apache2

Change the first line of */etc/apache2/sites-available/default* to 

	NameVirtualHost *:80
	<VirtualHost *:80>

Create host config file */etc/apache2/sites-available/gaiamobile.org*

<script src="https://gist.github.com/2641287.js"> </script>

Run the following commands in order

	sudo a2enmod expires
	sudo a2enmod vhost_alias
	sudo a2ensite gaiamobile.org
	sudo apache2ctl graceful

We need to modify Vagrant configure file t visit apache from local machine. Add
the next line in *Vagrant*

	config.vm.forward_port 80, 4567

And run *vagrant reload*. Then we can visit 127.0.0.1:4567, and it will show *It
works* page.

To see real gaia interface, add following lines in */etc/hosts*

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

For more detail about hacking Gaia, please go to [gaia-hacking].

Mac-B2G-Desktop
========

If you are a lazy man like me and you are using Mac, maybe you like to have a
working B2G browser. @pauljt provides a build of b2g desktop for Mac OS in
[mac-b2g-desktop].

Finish
=======

The develop enviroment is built. Have fun.

P.S. Do not forget to *make profile* first in Gaia and provide profile location
when you start browser.

[Vagrant]: http://vagrantup.com/
[b2g-vagrant]: https://github.com/rhelmer/b2g-vagrant/
[vagrant-proxyssh]: https://github.com/kvs/vagrant-proxyssh
[sshfs]: http://fuse.sourceforge.net/sshfs.html
[gaia-hacking]: https://wiki.mozilla.org/Gaia/Hacking
[mac-b2g-desktop]: https://github.com/pauljt/mac-b2g-desktop
