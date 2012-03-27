--- 
layout: post
title: !binary |
  6Kej5YazVkxDIE1lZGlhIFBsYXllciDkuK3mloflrZfluZXkubHnoIHnmoTp
  l67popg=

published: true
meta: {}

tags: 
- Software
- Ubuntu
type: post
status: publish
---
<a class="tt-flickr tt-flickr-Medium" title="vlc" href="http://www.flickr.com/photos/kylewu/3998103185/"><img class="alignnone" src="http://farm3.static.flickr.com/2660/3998103185_4b9b2ebd08.jpg" alt="vlc" width="1" height="1" /></a> 重装了一次Ubuntu，带来一个问题。本来VLC Player放电影时字幕没有问题，改成GTK就可以正常显示。但是这次重装以后，仅修改encoding不起作用。搜了很多网页，主要就是修改encoding，并且把字体改为中文字体。不过最后通过Ubuntu Wiki搞定了。

方法就是进入/etc/fonts/conf.d/文件夹，修改49-sansserif.conf这个文件。将最后一个看到的字体改为一个中文字体，我改为了WenQuanYi Zen Hei。

<code lang="xml">
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<!--
  If the font still has no generic name, add sans-serif
 -->
	<match target="pattern">
		<test qual="all" name="family" compare="not_eq">
			<string>sans-serif</string>
		</test>
		<test qual="all" name="family" compare="not_eq">
			<string>serif</string>
		</test>
		<test qual="all" name="family" compare="not_eq">
			<string>monospace</string>
		</test>
		<edit name="family" mode="append_last">
			<string>WenQuanYi Zen Hei</string>
		</edit>
	</match>
</fontconfig>
</code>

就是这么简单。Wiki的地址在<a href="http://wiki.ubuntu.org.cn/Vlc">这里</a>。
