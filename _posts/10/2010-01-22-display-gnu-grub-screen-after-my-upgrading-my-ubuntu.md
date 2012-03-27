--- 
layout: post
title: Display Gnu Grub screen after my upgrading my Ubuntu
published: true
meta: {}

tags: 
- OS
- Ubuntu
type: post
status: publish
---
<a class="tt-flickr tt-flickr-Medium" title="GRUB_screenshot" href="http://www.flickr.com/photos/kylewu/4294645799/"><img class="alignnone" src="http://farm5.static.flickr.com/4006/4294645799_c7940bd8a2.jpg" alt="GRUB_screenshot" width="1" height="1" /></a> <a title="Wubi" href="http://wubi-installer.org/">Wubi</a> is a great tool which can help you install Ubuntu in Windows without changing partition. I installed Ubuntu by using Wubi. Really easy!

But, after I upgraded Ubuntu and rebooted, there was no Ubuntu login windows. What I saw is a black screen. It said GNU Grub, Minimal Bash-like shell blabla. I have to say I don't like it, and you won't, either.

Luckily, it is easy to find a solution. I searched 'wubi ubuntu gnu grub' in Google. <a href="http://ubuntuforums.org/showthread.php?t=1321107"></a>The author of Wubi showed his solution <a href="https://bugs.launchpad.net/ubuntu/+source/lupin/+bug/477169/comments/210">here</a> :
<blockquote>For a patch/workaround:

A) get the wubildr in <a rel="nofollow" href="https://bugs.edge.launchpad.net/ubuntu/+source/grub2/+bug/477104/comments/90">https://bugs.edge.launchpad.net/ubuntu/+source/grub2/+bug/477104/comments/90</a> and copy it over C:wubildr
B) ensure that when you boot there is no command "insmod ntfs". Press "e" at the grub boot menu to edit the relevant entry and remove "insmod ntfs" before proceeding

New ubuntu/wubi installations do not contain the patch yet. The patch will only be applied once there is a clear confirmation (from you) that it actually solves the problem. Hence your feedback is appreciated.</blockquote>
Right, that's it, download that file and copy it over. There are also some other solutions in which you need to type lots of commands in command line. I think, the solution of his, the author of Wubi, is better :)
