--- 
layout: post
title: "Fix 'Taglist: Failed to generate tags' in Vim"
published: true
meta: {}

tags: 
- Software
- Vim
type: post
status: publish
---
When open taglist in vim, it may says:
<blockquote>Taglist: Failed to generate tags for /my/path/to/file
ctags: illegal option -- -^@usage: ctags [-BFadtuwvx] [-f tagsfile] file ...</blockquote>
Solution is quite easy, open .vimrc and add the following line
<blockquote>let Tlist_Ctags_Cmd='/location/ctags'</blockquote>
In my mbp, Snow Leopard, it is '/opt/local/var/macports/software/ctags/5.8_0/opt/local/bin/ctags' 
