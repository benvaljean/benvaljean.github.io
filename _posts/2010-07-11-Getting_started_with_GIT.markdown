---
layout: post 
title: Getting started with GIT
---

[http://git-scm.com GIT] is a relatively new Version Control System originally by Linus himself that has different principals to [[CVS]] and [[SVN]].

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
===Reverting a commit===
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


===References===
http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository
