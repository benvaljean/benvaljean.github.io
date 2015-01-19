---
layout: post 
title: Getting started with GIT
---

===Setup Client Environment===
<pre>
git config --global user.name "Joe Bloggs"
git config --global user.email email@email.com
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
</pre>

===GIT vs SVN cheat-sheet===

{| {{table}}
| align="center" style="background:#f0f0f0;"|'''GIT'''
| align="center" style="background:#f0f0f0;"|'''SVN'''
|-
| git clone repo||svn co repo
|-
| git pull||svn up
|}

===Create new repo===
Cd to the dir where version tracking is required and create the repo:
<pre>git init</pre>
Version track *.sh and *.pl files:
<pre>git add *.pl
git add *.sh</pre>
Perform your first commit:
<pre>git commit -m "Initial commit"</pre>
Re-commit every time changes are made:
<pre>git commit -a -m "test1"</pre>
===Diffs===
====Changes in working tree not yet staged for commit====
<pre>
git diff        </pre>
====Changes between staged changes and the working tree====    
<pre>git diff --cached</pre>

====Changes in the working tree since your last commit====
<pre>git diff HEAD</pre>

http://git-scm.com/docs/git-diff

===Reverting===
====Reverting local changes====
Revert local changes to the version on the same branch of the most recent commit:<ref>http://stackoverflow.com/questions/692246/undo-working-copy-modifications-of-one-file-in-git</ref>
<pre>
git checkout HEAD -- file</pre>
Revert local changes to the version on the same branch of the commit directly BEFORE the most recent commit:<ref>http://stackoverflow.com/questions/692246/undo-working-copy-modifications-of-one-file-in-git</ref>
<pre>git checkout HEAD^ -- file </pre>
====Reverting a commit====
Use <tt>git log</tt> to view the list of commits, note the long alpha-numeric after "commit".
<pre>git revert <commit-number></pre>

===Setup remote repo===
Setup a bare remote repo:
<pre>ssh remote-server
mkdir -p /var/git/repo1
cd /var/git/repo1
git --bare init
exit
</pre>
In your new repo folder:
<pre>git remote add origin ssh://remote-server/var/git/repo1</pre>
The following command will now push your repo to remote-server:<pre>git push origin master</pre>
===Clone an existing repo===
Note that the term 'check-out' is specifically not used here, as 'check out' in GIT is completely different to 'check-out' in CVS/SVN. A check-out in CVS/SVN is called 'clone' in GIT.
<pre>git glone http://blah.com/repos/bgrepo.git</pre>
Repos can also be setup using GITs own protocol in the form of <tt>git clone git://...</tt> or over SSH as described above or with <tt>git clone user@host:repos/bgrepo.git</tt>
===Making stages===
GIT unlike CVS/SVN has a 'staging' principal. Changes that are made to files in your local repo are not automatically committed when <tt>git commit</tt> is run. All local changes must be set to be 'ready to commit' instead, which is is called 'staging' in SVN-speak. This is done from the <tt>git add</tt> which is also used to add files to the repo as in CVS/SVN. Local changes made since <tt>git add</tt> was run will NOT be committed! Instead the changes up to the last time <tt>git add</tt> was run on the file are committed. This is an important point as this is very different to the principals behind CVS/SVN and indeed other VCS.

It is possible to force git to place all local changes into staging before the commit ala CVS/SVN with the <tt>-a</tt> argument. This will place into staging files which already tracked - <tt>git add</tt> is only required to add new tracked files to the repo.
===Renaming files===
GIT does not automatically track file renames, however if a file is removed and re-added to the repo the change history is still retained.
*Both of these commands have the same result:
<pre>
git mv script.pl script2.pl</pre>
<pre>
mv script.pl script2.pl
git rm script.pl
git add script2.pl</pre>

===Branching and merging===
A branch is a separate snapshot of your primary or <tt>master</tt> branch that can be worked out with affecting the <tt>master</tt> branch.
<pre>
$ git branch
* master
$ git checkout -b fix-fallback
Switched to a new branch 'fix-fallback'
$ vim index.html
$ git commit -a -m 'fixed fallback'
[fix-fallback 3a0874c] fixed fallback
 1 files changed, 1 deletion(-)
</pre>
Now they changes are committed in the fix-fallback branch. To merge this into <tt>master</tt> we switch to it and perform a <tt>merge</tt> command:
<pre>
$ git checkout master
$ git merge fix-fallback
Updating f42c576..3a0874c
Fast-forward
 ....
 1 file changed
</pre>
Now that the changes have been merged into <tt>master</tt> the fix-fallback branch can be deleted:
<pre>
$ git branch -d fix-fallback
</pre>
===Logs===
===List changes in this branch===
<pre>
git cherry -v</pre>
OR
<pre>
git log <upsteam-branch>..</pre>
====See changes in last commit====
<pre>
git log --name-status HEAD^..HEAD
</pre>
<ref>http://stackoverflow.com/questions/2231546/git-see-my-last-commit</ref>
====See changes in a given commit id====
<pre>
git show <commit-id>
</pre>

===References===
http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository

http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging

<references/>
