--- 
layout: post
title: Intro to Distributed Version Control (Illustrated)
published: true
meta: {}

tags: 
- cvs
- IT
- mercurial
- Software
- svn
- tutorial
- Web
type: post
status: publish
---
上篇介绍版本控制，这篇介绍了分布式的版本控制，与集中式vc相比，分布式vc有很多好处。

<img src="http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_logo.png" alt="" />

Traditional version control helps you backup, track and synchronize files. Distributed version control makes it easy to share changes. Done right, you can get the best of both worlds: simple merging and centralized releases.
<h2>Distributed? What’s wrong with regular version control?</h2>
<!--more-->

Nothing — read <a href="http://betterexplained.com/articles/a-visual-guide-to-version-control/">a visual guide to version control</a> if you want a quick refresher. Sure, <em>some people</em> will deride you for using an “ancient” system. But you’re still OK in my book: using <em>any</em> <span class="caps">VCS </span>is a positive step forward for a project.

Centralized <span class="caps">VCS </span>emerged from the 1970s, when programmers had thin clients and admired “big iron” mainframes (how can you <strong>not</strong> like a machine with a then-gluttonous <a onclick="javascript:urchinTracker ('/outbound/en.wikipedia.org');" href="http://en.wikipedia.org/wiki/System/360">8 bits to a byte</a>?).

<strong>Centralized is simple</strong>, and what you’d first invent: a single place everyone can check in and check out. It’s like a library where you get to scribble in the books.

This model works for <strong>backup, undo and synchronization</strong> but isn’t great for <strong>merging and branching</strong> changes people make. As projects grow, you want to split features into chunks, developing and testing in isolation and slowly merging changes into the main line. In reality, branching is cumbersome, so new features may come as a giant checkin, making changes difficult to manage and untangle if they go awry.

Sure, merging is always “possible” in a centralized system, but it’s not easy: you often need to track the merge yourself to avoid making the same change twice. Distributed systems make branching and merging painless because they rely on it.
<div class="textad sponsored_footer" style="display: none;"><span class="meta">Advertisement:</span> Use <a onclick="javascript:urchinTracker('/ads/springloops.com');" rel="nofollow" href="http://springloops.com/">Springloops</a> for your secure and rapid web deployment. Easily share and deploy your code. Free & paid plans and no contracts: Try it today!</div>
<h2>A Few Diagrams, Please</h2>
Other tutorials have plenty of nitty-gritty text commands; here’s a <strong>visual</strong> look. To refresh, developers use a central repo in a typical <span class="caps">VCS</span>:

<img src="http://betterexplained.com/wp-content/uploads/version_control/distributed/centralized_example.png" alt="" />

Everyone syncs and checks into the main trunk: Sue adds soup, Joe adds juice, and Eve adds eggs.

Sue’s change must go into main before it can be seen by others. Yes, theoretically Sue <em>could</em> make a new branch for other people to try out her changes, but this is a pain in a regular <span class="caps">VCS.</span>
<h2>Distributed Version Control Systems (DVCS)</h2>
In a <strong>distributed</strong> model, every developer has their own repo. Sue’s changes live in <strong>her local repo</strong>, which she can share with Joe or Eve:

<img src="http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_example.png" alt="" />

But will it be a circus with no ringleader? Nope. If desired, everyone can push changes into a common repo, suspiciously like the centralized model above. This franken-repo contains the changes of Sue, Joe and Eve.

<strong>I wish distributed version control had a different name</strong>, such as “independent”, “federated” or “peer-to-peer.” The term “distributed” evokes thoughts of distributed computing, where work is split among a grid of machines (like searching for signals with <a onclick="javascript:urchinTracker ('/outbound/setiathome.berkeley.edu');" href="http://setiathome.berkeley.edu/"><span class="caps">SETI</span>@home</a> or doing <a onclick="javascript:urchinTracker ('/outbound/folding.stanford.edu');" href="http://folding.stanford.edu/">protein folding</a>).

A <span class="caps">DVCS </span>is not like Seti@home: each node is completely independent and sharing is optional (in Seti you must phone back your results).
<h2>Key Concepts In 5 Minutes</h2>
Here’s the basics; there’s a <a onclick="javascript:urchinTracker ('/outbound/en.wikibooks.org');" href="http://en.wikibooks.org/wiki/Understanding_darcs/Patch_theory">book</a> on patch theory if you’re interested.

<strong>Core Concepts</strong>
<ul>
	<li>Centralized version control focuses on <strong>synchronizing, tracking, and backing up files.</strong></li>
	<li>Distributed version control focuses on <strong>sharing changes</strong>; every change has a <a href="http://betterexplained.com/articles/the-quick-guide-to-guids/">guid or unique id</a>.</li>
	<li><strong>Recording/Downloading</strong> and <strong>applying</strong> a change are separate steps (in a centralized system, they happen together).</li>
	<li><strong>Distributed systems have no forced structure</strong>. You can create “centrally administered” locations or keep everyone as peers.</li>
</ul>
<strong>New Terminology</strong>
<ul>
	<li><strong>push</strong>: send a change to another repository (may require permission)</li>
	<li><strong>pull</strong>: grab a change from a repository</li>
</ul>
<strong>Key Advantages</strong>
<ul>
	<li><strong>Everyone has a local sandbox.</strong> You can make changes and roll back, all on your local machine. No more giant checkins; your incremental history is in your repo.</li>
	<li><strong>It works offline.</strong> You only need to be online to share changes. Otherwise, you can happily stay on your local machine, checking in and undoing, no matter if the “server” is down or you’re on an airplane.</li>
	<li><strong>It’s fast.</strong> Diffs, commits and reverts are all done locally. There’s no shaky network or server to ask for old revisions from a year ago.</li>
	<li><strong>It handles changes well.</strong> Distributed version control systems were <em>built</em> around sharing changes. Every change has a guid which makes it easy to track.</li>
	<li><strong>Branching and merging is easy.</strong> Because every developer “has their own branch”, every shared change is like reverse integration. But the guids make it easy to automatically combine changes and avoid duplicates.</li>
	<li><strong>Less management.</strong> Distributed <span class="caps">VCS</span>es are easy to get running; there’s no “always-running” server software to install. Also, <span class="caps">DVCS</span>es may not require you to “add” new users; you just pick what <span class="caps">URL</span>s to pull from. This can avoid political headaches in large projects.</li>
</ul>
<strong>Key Disadvantages</strong>
<ul>
	<li><strong>You still need a backup.</strong> Some claim your “backup” is the other machines that have your changes. I don’t buy it — what if they didn’t accept them all? What if they’re offline and you have new changes? With a <span class="caps">DVCS, </span>you still want a machine to push changes to “just in case”. (In Subversion, you usually dedicate a machine to store the main repo; do the same for a <span class="caps">DVCS</span>).</li>
	<li><strong>There’s not really a “latest version”</strong>. If there’s no central location, you don’t immediately know whether to see Sue, Joe or Eve for the latest version. Again, a central location helps clarify what the latest “stable” release is.</li>
	<li><strong>There aren’t really revision numbers.</strong> Every repo has its own revision numbers depending on the changes. Instead, people refer to change numbers: <em>Pardon me, do you have change fa33e7b?</em> (Remember, the id is an ugly guid). Thankfully, you can tag releases with meaningful names.</li>
</ul>
<h2>Mercurial Quickstart</h2>
Mercurial is a fast, simple <span class="caps">DVCS.</span> The nickname is hg, like the element Mercury.
<pre><code>
cd project
hg init                                (create repo here)
hg add list.txt                        (start tracking file)
hg commit -m "Added file"              (check file into local repo)
hg log                                 (see history; notice guid)

changeset:   0:55bbcb7a4c24
user:        Kalid@kazad-laptop
date:        Sun Oct 14 21:36:18 2007 -0400
summary:     Added file

[edit file]
hg revert list.txt                 (revert to previous version)

hg tag v1.0                        (tag this version)
[edit file]
hg update -C v1.0                  ("update" to the older tagged version; -C forces overwrite of local copy)
</code></pre>
Once Mercurial has initialized a directory, it looks like this:

<img src="http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_repo_layout.png" alt="" />

You have:
<ul>
	<li><strong>A working copy</strong>. The files you are currently editing.</li>
	<li><strong>A repository</strong>. A directory (.hg in Mercurial) containing all patches and metadata (comments, guids, dates, etc.). There’s no central server so the data stays with you.</li>
</ul>
In our distributed example, Sue, Joe and Eve have their own repos, with independent revision histories.
<h2>Understanding Updates and Merging</h2>
There’s a few items that confused me when learning about <span class="caps">DVCS.</span> First, updates happen in several steps:
<ul>
	<li><strong>Getting</strong> the change into a repo (pushing or pulling)</li>
	<li><strong>Applying</strong> the change to the files (update or merge)</li>
	<li><strong>Saving</strong> the new version (commit)</li>
</ul>
Second, depending on the change, you can update or merge:
<ul>
	<li><strong>Updates</strong> happen when there’s no ambiguity. For example, I pull changes to a file that only you’ve been editing. The file just jumps to the latest revision, since there’s no overlapping changes.</li>
	<li><strong>Merges</strong> are needed when we have conflicting changes. If we both edit a file, we end up with two “branches” (i.e. alternate universes). One world has my changes, the other world has yours. In this case we (probably) want to merge the changes together into a single universe.</li>
</ul>
I’m still wrapping my head around how easily branches spring up and collapse in a <span class="caps">DVCS</span>:

<img src="http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_merge.png" alt="" />

In this case, a merge is needed because (+Soup) and (+Juice) are changes to a common parent: the list with just “Milk”. After Joe merges the files, Sue can do a regular “pull and update” to get the combined file from Joe. She doesn’t have to merge again on her own.

In Mercurial you can run:
<pre><code>
hg incoming ../another-dir  (see pending changes)
hg pull ../another-dir      (download changes)

hg update                   (actually apply changes...)
hg merge                    (... or merge if needed)

hg commit                   (check in merged file; unite branches)
</code></pre>
Yep, the “pull-merge-commit” cycle is long. Luckily, Mercurial has shortcuts to combine commands into a single one. Though it seems complex, it’s <strong>much</strong> easier than handling merges manually in Subversion.

<strong>Most merges are automatic.</strong> When conflicts come up, they are typically resolved quickly. Mercurial keeps track of the parent/child relationship for every change (our merged list has two parents), as well as the “heads” or latest changes in each branch. Before the merge we have two heads; afterwards, one.
<h2>Organizing a Distributed Project</h2>
Here’s one way to organize a distributed project:

<img src="http://betterexplained.com/wp-content/uploads/version_control/distributed/distributed_push_pull.png" alt="" />

Sue, Joe and Eve check changes into a common branch. They can trade patches with each other to do simple <strong>“buddy builds”</strong>: <em>Hey buddy, can you try out these patches? I need to see if it works before I push to the experimental branch.</em>

Later, a maintainer can review and pull changes from the experimental branch into a stable branch, which has the latest release. A distributed <span class="caps">VCS </span>helps isolate changes but still provide the “single source” of a centralized system. There are many models of development, from “pull only” (where maintainers decide what to take, and is used when developing Linux) to “shared push” (which acts like a centralized system). A distributed <span class="caps">VCS </span>gives you <strong>flexibility</strong> in how a project is maintained.
<h2>Practice And Scathing Ridicule Makes Perfect</h2>
I’m a <span class="caps">DVCS </span>newbie, but am happy with what I’ve learned so far. I enjoy <span class="caps">SVN, </span>but it’s “fun” seeing how easy a merge can be. My suggestion is to start with Subversion, get a grasp for team collaboration, then experiment with a distributed model. With the proper layout a <span class="caps">DVCS </span>can do anything a centralized system can, with the added benefit of easy merging.

<strong>Online Resources</strong>
<ul>
	<li><a onclick="javascript:urchinTracker ('/outbound/www.selenic.com');" href="http://www.selenic.com/mercurial/wiki/">Mercurial</a> has an <a onclick="javascript:urchinTracker ('/outbound/hgbook.red-bean.com');" href="http://hgbook.red-bean.com/hgbook.html">excellent book</a>. On Windows you may need <a onclick="javascript:urchinTracker ('/outbound/kdiff3.sourceforge.net');" href="http://kdiff3.sourceforge.net/">diffing/merging software</a> or <a onclick="javascript:urchinTracker ('/outbound/tortoisesvn.tigris.org');" href="http://tortoisesvn.tigris.org/TortoiseMerge.html">TortoiseMerge</a> (if you have TortoiseSVN installed).</li>
	<li><a onclick="javascript:urchinTracker ('/outbound/darcs.net');" href="http://darcs.net/">Darcs</a> has a detailed <a onclick="javascript:urchinTracker ('/outbound/en.wikibooks.org');" href="http://en.wikibooks.org/wiki/Understanding_darcs">wikibook</a> (has some math theory about changes).</li>
	<li><a onclick="javascript:urchinTracker ('/outbound/git.or.cz');" href="http://git.or.cz/">Git</a> was created by Linus Torvalds. Here’s an <a onclick="javascript:urchinTracker ('/outbound/www.youtube.com');" href="http://www.youtube.com/watch?v=4XpnKHJAok8">interesting lecture</a> on <span class="caps">DVCS</span>; prepare to be berated for using a centralized system: (Youtube视频，国内可能看不到)<object width="425" height="350" data="http://www.youtube.com/v/4XpnKHJAok8" type="application/x-shockwave-flash"><param name="wmode" value="transparent" /><param name="src" value="http://www.youtube.com/v/4XpnKHJAok8" /></object></li>
</ul>


Notable Quotes:
<ul>
	<li>“How many have done a branch and merged it? How many of you enjoyed it?”</li>
	<li>“When you do a merge, you plan ahead for a week, then set aside a day to do it.”</li>
	<li>“Some people have 5, 10, 15 branches”. One branch is experimental. One branch is maintenance, etc.</li>
	<li>“CVS — you don’t commit. You make changes without committing. You never commit until it passes a giant test suite. People make 1-liner changes, knowing it can’t <em>possibly</em> break.”</li>
</ul>
So good luck, and watch out for the holy wars. Feel free to share any tips or suggestions below.

This article is from betterexplained.com. Here is the <a title="Intro to Distributed Version Control (Illustrated)" href="http://betterexplained.com/articles/intro-to-distributed-version-control-illustrated/" target="_blank">Source</a>.
