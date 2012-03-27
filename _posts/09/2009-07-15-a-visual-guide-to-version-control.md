--- 
layout: post
title: A Visual Guide to Version Control
published: true
meta: {}

tags: 
- cvs
- IT
- Software
- svn
- tutorial
type: post
status: publish
---
这篇文章介绍了Version Control版本控制的一些基本概念。

<img src="http://betterexplained.com/wp-content/uploads/version_control/version_control_intro_small.png" border="0" alt="" align="center" />

Version Control (aka Revision Control aka Source Control) lets you track your files over time. Why do you care? So when you mess up you can easily get back to a previous working version.

<strong>You’ve probably cooked up your own</strong> version control system without realizing it had such a geeky name. Got any files like this? (Not these exact ones I hope).
<ul>
	<li>KalidAzadResumeOct2006.doc</li>
	<li>KalidAzadResumeMar2007.doc</li>
	<li>instacalc-logo3.png</li>
	<li>instacalc-logo4.png</li>
	<li>logo-old.png</li>
</ul>
<strong>It’s why we use “Save As”.</strong> You want the new file without obliterating the old one. It’s a common problem, and solutions are usually like this:
<ul>
	<li>Make a <strong>single backup copy</strong> (Document.old.txt).</li>
	<li>If we’re clever, we add a <strong>version number or date</strong>: Document_V1.txt, DocumentMarch2007.txt</li>
	<li>We may even use a <strong>shared folder</strong> so other people can see and edit files without sending them over email. Hopefully they relabel the file after they save it.</li>
</ul>
<!--more-->
<div class="textad sponsored_footer" style="display: none;"><span class="meta">Advertisement:</span> Use <a onclick="javascript:urchinTracker('/ads/springloops.com');" rel="nofollow" href="http://springloops.com/">Springloops</a> for your secure and rapid web deployment. Easily share and deploy your code. Free & paid plans and no contracts: Try it today!</div>
<h2>So Why Do We Need A Version Control System (VCS)?</h2>
Our shared folder/naming system is fine for class projects or one-time papers. But software projects? Not a chance.

Do you think the Windows source code sits in a shared folder like “Windows2007-Latest-UPDATED!!”, for anyone to edit? That every programmer just works in a different subfolder? No way.

Large, fast-changing projects with many authors need a Version Control System (geekspeak for “file database”) to track changes and avoid general chaos. A good <span class="caps">VCS </span>does the following:
<ul>
	<li><strong>Backup and Restore.</strong> Files are saved as they are edited, and you can jump to any moment in time. Need that file as it was on Feb 23, 2007? No problem.</li>
	<li><strong>Synchronization.</strong> Lets people share files and stay up-to-date with the latest version.</li>
	<li><strong>Short-term undo.</strong> Monkeying with a file and messed it up? (That’s just like you, isn’t it?). Throw away your changes and go back to the “last known good” version in the database.</li>
	<li><strong>Long-term undo.</strong> Sometimes we mess up bad. Suppose you made a change a year ago, and it had a bug. Jump back to the old version, and see what change was made that day.</li>
	<li><strong>Track Changes</strong>. As files are updated, you can leave messages explaining why the change happened (stored in the <span class="caps">VCS, </span>not the file). This makes it easy to see how a file is evolving over time, and why.</li>
	<li><strong>Track Ownership.</strong> A <span class="caps">VCS </span>tags every change with the name of the person who made it. Helpful for <a onclick="javascript:urchinTracker ('/outbound/www.unwords.com');" href="http://www.unwords.com/unword/blamestorming.html"><del>blamestorming</del></a> giving credit.</li>
	<li><strong>Sandboxing</strong>, or insurance against yourself. Making a big change? You can make temporary changes in an isolated area, test and work out the kinks before “checking in” your changes.</li>
	<li><strong>Branching and merging</strong>. A larger sandbox. You can <strong>branch</strong> a copy of your code into a separate area and modify it in isolation (tracking changes separately). Later, you can <strong>merge</strong> your work back into the common area.</li>
</ul>
Shared folders are quick and simple, but can’t beat these features.
<h2>Learn the Lingo</h2>
Most version control systems involve the following concepts, though the labels may be different.

Basic Setup
<ul>
	<li><strong>Repository (repo)</strong>: The database storing the files.</li>
	<li><strong>Server</strong>: The computer storing the repo.</li>
	<li><strong>Client</strong>: The computer connecting to the repo.</li>
	<li><strong>Working Set/Working Copy</strong>: Your local directory of files, where you make changes.</li>
	<li><strong>Trunk/Main</strong>: The “primary” location for code in the repo. Think of code as a family tree — the “trunk” is the main line.</li>
</ul>
Basic Actions
<ul>
	<li><strong>Add</strong>: Put a file into the repo for the first time, i.e. begin tracking it with Version Control.</li>
	<li><strong>Revision</strong>: What version a file is on (v1, v2, v3, etc.).</li>
	<li><strong>Head</strong>: The latest revision in the repo.</li>
	<li><strong>Check out</strong>: Download a file from the repo.</li>
	<li><strong>Check in</strong>: Upload a file to the repository (if it has changed). The file gets a new revision number, and people can “check out” the latest one.</li>
	<li><strong>Checkin Message</strong>: A short message describing what was changed.</li>
	<li><strong>Changelog/History</strong>: A list of changes made to a file since it was created.</li>
	<li><strong>Update/Sync</strong>: Synchronize your files with the latest from the repository. This lets you grab the latest revisions of all files.</li>
	<li><strong>Revert</strong>: Throw away your local changes and reload the latest version from the repository.</li>
</ul>
Advanced Actions
<ul>
	<li><strong>Branch</strong>: Create a separate copy of a file/folder for private use (bug fixing, testing, etc). Branch is both a verb (”branch the code”) and a noun (”Which branch is it in?”).</li>
	<li><strong>Diff/Change/Delta</strong>: Finding the differences between two files. Useful for seeing what changed between revisions.</li>
	<li><strong>Merge (or patch)</strong>: Apply the changes from one file to another, to bring it up-to-date. For example, you can merge features from one branch into another. (At Microsoft this was called <a onclick="javascript:urchinTracker ('/outbound/blogs.msdn.com');" href="http://blogs.msdn.com/larryosterman/archive/2005/02/01/364840.aspx">Reverse Integrate and Forward Integrate</a>)</li>
	<li><strong>Conflict</strong>: When pending changes to a file contradict each other (both changes cannot be applied).</li>
	<li><strong>Resolve</strong>: Fixing the changes that contradict each other and checking in the correct version.</li>
	<li><strong>Locking</strong>: “Taking control” of a file so nobody else can edit it until you unlock it. Some version control systems use this to avoid conflicts.</li>
	<li><strong>Breaking the lock</strong>: Forcibly unlocking a file so you can edit it. It may be needed if someone locks a file and goes on vacation (or “calls in sick” the day Halo 3 comes out).</li>
	<li><strong>Check out for edit</strong>: Checking out an “editable” version of a file. Some <span class="caps">VCS</span>es have editable files by default, others require an explicit command.</li>
</ul>
And a typical scenario goes like this:

Alice <strong>adds</strong> a file (<code>list.txt</code>) to the <strong>repository</strong>. She <strong>checks it out</strong>, makes a change (puts “milk” on the list), and checks it back in with a checkin message (”Added required item.”). The next morning, Bob <strong>updates</strong> his local working set and sees the latest revision of <code>list.txt</code>, which contains “milk”. He can browse the <strong>changelog</strong> or <strong>diff</strong> to see that Alice put “milk” the day before.
<h2>Visual Examples</h2>
This guide is purposefully high-level: most tutorials throw a bunch of text commands at you. Let’s cover the high-level concepts without getting stuck in the syntax (the <a onclick="javascript:urchinTracker ('/outbound/svnbook.red-bean.com');" href="http://svnbook.red-bean.com/">Subversion manual</a> is always there, don’t worry). Sometimes it’s nice to <strong>see what’s possible</strong>.
<h2>Checkins</h2>
The simplest scenario is checking in a file (<code>list.txt</code>) and modifying it over time.

<img src="http://betterexplained.com/wp-content/uploads/version_control/basic_checkin.png" alt="version control checkin" />

Each time we check in a new version, we get a new revision (r1, r2, r3, etc.). In Subversion you’d do:
<pre><code>svn add list.txt
(modify the file)
svn ci list.txt -m "Changed the list"</code></pre>
The <code>-m</code> flag is the message to use for this checkin.
<h2>Checkouts and Editing</h2>
In reality, you might not keep checking in a file. You may have to <strong>check out, edit and check in</strong>. The cycle looks like this:

<img src="http://betterexplained.com/wp-content/uploads/version_control/checkout_edit.png" alt="version control checkout" />

If you don’t like your changes and want to start over, you can <strong>revert</strong> to the previous version and start again (or stop). When checking out, you get the latest revision by default. If you want, you can specify a particular revision. In Subversion, run:
<pre><code>
svn co list.txt (get latest version)
...edit file...
svn revert list.txt (throw away changes)

svn co -r2 list.txt (check out particular version)
</code></pre>
<h2>Diffs</h2>
The trunk has a history of <strong>changes</strong> as a file evolves. Diffs are the changes you made while editing: imagine you can “peel” them off and apply them to a file:

<img src="http://betterexplained.com/wp-content/uploads/version_control/basic_diffs.png" alt="version control diff" />

For example, to go from r1 to r2, we add eggs (+Eggs). Imagine peeling off that red sticker and placing it on r1, to get r2.

And to get from r2 to r3, we add Juice (+Juice). To get from r3 to r4, we remove Juice and add Soup (-Juice, +Soup).

Most version control systems <strong>store diffs rather than full copies of the file</strong>. This saves disk space: 4 revisions of a file doesn’t mean we have 4 copies; we have 1 copy and 4 small diffs. Pretty nifty, eh? In <span class="caps">SVN, </span>we diff two revisions of a file like this:
<pre><code>svn diff -r3:4 list.txt</code></pre>
Diffs help us notice changes (”How did you fix that bug again?”) and even apply them from one branch to another.

<strong>Bonus question:</strong> what’s the diff from r1 to r4?
<pre><code>+Eggs
+Soup</code></pre>
Notice how “Juice” wasn’t even involved — the direct jump from r1 to r4 doesn’t need that change, since Juice was overridden by Soup.
<h2>Branching</h2>
Branches let us copy code into a separate folder so we can monkey with it separately:

<img src="http://betterexplained.com/wp-content/uploads/version_control/first_branch.png" alt="version control branch" />

For example, we can create a branch for new, experimental ideas for our list: crazy things like Rice or Eggo waffles. Depending on the version control system, creating a branch (copy) may change the revision number.

Now that we have a branch, we can change our code and work out the kinks. (<em>“Hrm… waffles? I don’t know what the boss will think. Rice is a safe bet.”</em>). Since we’re in a separate branch, we can make changes and test in isolation, knowing our changes won’t hurt anyone. And our branch history is under version control.

In Subversion, you create a branch simply by copying a directory to another.
<pre><code>svn copy http://path/to/trunk http://path/to/branch</code></pre>
So branching isn’t too tough of a concept: <strong>Pretend you copied your code into a different directory.</strong> You’ve probably branched your code in school projects, making sure you have a “fail safe” version you can return to if things blow up.
<h2>Merging</h2>
Branching sounds simple, right? Well, it’s not — figuring out how to merge changes from one branch to another can be tricky.

Let’s say we want to get the “Rice” feature from our experimental branch into the mainline. How would we do this? Diff r6 and r7 and apply that to the main line?

<strong>Wrongo.</strong> We only want to apply the changes <strong>that happened in the branch!</strong>. That means we diff r5 and r6, and apply that to the main trunk:

<img src="http://betterexplained.com/wp-content/uploads/version_control/merging.png" alt="version control merge" />

If we diffed r6 and r7, we would lose the “Bread” feature that was in main. This is a subtle point — imagine “peeling off” the changes from the experimental branch (+Rice) and adding that to main. Main may have had other changes, which is ok — we just want to insert the Rice feature.

In Subversion, merging is very close to diffing. Inside the main trunk, run the command:
<pre><code>svn merge -r5:6 http://path/to/branch</code></pre>
This command diffs r5-r6 in the experimental branch and applies it to the current location. Unfortunately, Subversion doesn’t have an easy way to keep track of what merges have been applied, so if you’re not careful you may apply the same changes twice. It’s a planned feature, but the current advice is to keep a changelog message reminding you that you’ve already merged r5-r6 into main.
<h2>Conflicts</h2>
Many times, the <span class="caps">VCS </span>can automatically merge changes to different parts of a file. <strong>Conflicts</strong> can arise when changes appear that don’t gel: Joe wants to remove eggs and replace it with cheese (-eggs, +cheese), and Sue wants to replace eggs with a hot dog (-eggs, +hot dog).

<img src="http://betterexplained.com/wp-content/uploads/version_control/vcs_conflict.png" alt="version control conflict" />

At this point it’s a race: if Joe checks in first, that’s the change that goes through (and Sue can’t make her change).

When changes overlap and contradict like this, the <span class="caps">VCS </span>may report a <strong>conflict</strong> and not let you check in — it’s up to you to check in a newer version that <strong>resolves</strong> this dilemma. A few approaches:
<ul>
	<li><strong>Re-apply your changes</strong>. Sync to the the latest version (r4) and re-apply your changes to this file: Add hot dog to the list that already has cheese.</li>
	<li><strong>Override their changes with yours</strong>. Check out the latest version (r4), copy over your version, and check your version in. In effect, this removes cheese and replaces it with hot dog.</li>
</ul>
Conflicts are infrequent but can be a pain. Usually I update to the latest and re-apply my changes.
<h2>Tagging</h2>
Who would have thought a version control system would be Web 2.0 compliant? Many systems let you tag (label) any revision for easy reference. This way you can refer to “Release 1.0″ instead of a particular build number:

<img src="http://betterexplained.com/wp-content/uploads/version_control/tagging.png" alt="version control tag" />

In Subversion, tags are just branches that you agree not to edit; they are around for posterity, so you can see exactly what your version 1.0 release contained. Hence they end in a stub — there’s nowhere to go.
<pre><code>(in trunk)
svn copy http://path/to/revision http://path/to/tag
</code></pre>
<h2>Real-life example: Managing Windows Source Code</h2>
We guessed that Windows was managed out of a shared folder, but it’s not the case. So <a onclick="javascript:urchinTracker ('/outbound/blogs.msdn.com');" href="http://blogs.msdn.com/larryosterman/archive/2005/02/01/364840.aspx">how’s it done</a>?
<ul>
	<li>There’s a <strong>main line</strong> with stable builds of Windows.</li>
	<li>Each group (Networking, User Interface, Media Player, etc.) <strong>has its own branch</strong> to develop new features. These are under development and less stable than main.</li>
</ul>
You develop new features in your branch and “Reverse Integrate (RI)” to get them into Main. Later, you “Forward Integrate” and to get the latest changes from Main into your branch:

<img src="http://betterexplained.com/wp-content/uploads/version_control/windows.png" alt="version control branch example" />

Let’s say we’re at Media Player 10 and IE 6. The Media Player team makes version 11 in their own branch. When it’s ready and tested, there’s a patch from 10 - 11 which is applied to Main (just like the “Rice” example, but a tad more complicated). This a <strong>reverse integration</strong>, from the branch to the trunk. The IE team can do the same thing.

Later, the Media Player team can pick up the latest code from other teams, like <span class="caps">IE.</span> In this case, Media Player <strong>forward integrates</strong> and gets the latest patches from main into their branch. This is like pulling in the “Bread” feature into the experimental branch, but again, more complicated.

So it’s RI and <span class="caps">FI.</span> Aye aye. This arrangement lets changes percolate throughout the branches, while keeping new code out of the main line. Cool, eh?

In reality, there’s many layers of branches and sub-branches, along with quality metrics that determine when you get to <span class="caps">RI.</span> But you get the idea: branches help manage complexity. Now you know the basics of how one of the largest software projects is organized.
<h2>Key Takeaways</h2>
My goal was to share high-level thoughts about version control systems. Here are the basics:
<ul>
	<li><strong>Use version control.</strong> Seriously, it’s a good thing, even if you’re not writing an <span class="caps">OS.</span> It’s worth it for backups alone.</li>
	<li><strong>Take it slow.</strong> I’m only now looking into branching and merging for my projects. Just get a handle on using version control and go from there. If you’re a small project, branching/merging may not be an issue. Large projects often have experienced maintainers who keep track of the branches and patches.</li>
	<li><strong>Keep Learning.</strong> There’s plenty of guides for <a onclick="javascript:urchinTracker ('/outbound/svnbook.red-bean.com');" href="http://svnbook.red-bean.com/"><span class="caps">SVN</span></a>, <a onclick="javascript:urchinTracker ('/outbound/wwwasd.web.cern.ch');" href="http://wwwasd.web.cern.ch/wwwasd/cvs/tutorial/cvs_tutorial_toc.html"><span class="caps">CVS</span></a>, <a onclick="javascript:urchinTracker ('/outbound/agave.garden.org');" href="http://agave.garden.org/%7Eaaronh/rcs/tutorial.html"><span class="caps">RCS</span></a>, Git, <a onclick="javascript:urchinTracker ('/outbound/public.perforce.com');" href="http://public.perforce.com/public/tutorial.html">Perforce</a> or whatever system you’re using. The important thing is to <strong>know the concepts</strong> and realize every system has its own lingo and philosophy. Eric Sink has a <a onclick="javascript:urchinTracker ('/outbound/www.ericsink.com');" href="http://www.ericsink.com/scm/source_control.html">detailed version control guide</a> also.</li>
</ul>
These are the basics — as time goes on I’ll share specific lessons I’ve learned from <a onclick="javascript:urchinTracker ('/outbound/instacalc.com');" href="http://instacalc.com/">my projects</a>. Now that you’ve figured out a regular <span class="caps">VCS, </span><a href="http://betterexplained.com/articles/intro-to-distributed-version-control-illustrated/">try an illustrated guide to distributed version control</a>.

This article is from betterexplained.com. Here is the <a title="A Visual Guide to Version Control" href="http://betterexplained.com/articles/a-visual-guide-to-version-control/" target="_blank">Source</a>.
