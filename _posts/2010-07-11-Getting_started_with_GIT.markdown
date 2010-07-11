---
layout: post 
title: Getting started with GIT
---

Cd to the dir where version tracking is required and creator the repo:
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
<pre>git revert <commit-number>
