--- 
layout: post
title: "\xE4\xBF\xAE\xE5\xA4\x8DUbuntu Jaunty\xE4\xB8\xAD\xE7\x9A\x84Ctrl+Alt+Backspace"
published: true
meta: {}

tags: 
- OS
type: post
status: publish
---
很多同学应该已经习惯了Ctrl+Alt+Backspace来重启X桌面。但是在Ubuntu Jaunty中，这个快捷键不起作用了。Ubuntu此举是为了避免用户误操作。从我个人来讲，没有了Ctrl+Alt+Backspace十分不方便。

恢复快捷键很方便：

安装dontzap
<pre class="bash" style="font-family: monospace;"><span style="color: #c20cb9; font-weight: bold;">sudo</span> <span style="color: #c20cb9; font-weight: bold;">apt-get</span> <span style="color: #c20cb9; font-weight: bold;">install</span> dontzap

Disable dontzap</pre>
<div class="wp_syntax">
<div class="code">
<pre class="bash" style="font-family: monospace;"><span style="color: #c20cb9; font-weight: bold;">sudo</span> dontzap <span style="color: #660033;">--disable</span></pre>
</div>
</div>
<pre class="bash" style="font-family: monospace;">重启电脑。

好了，你可以使用Ctrl+Alt+Backspace了。</pre>
