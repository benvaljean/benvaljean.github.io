---
layout: post 
title: Getting started with SVN
---

svnadmin create reponame

mkdir test touch test/test1.txt touch test/test2.txt

svn import dir <file:///full/path/to/dir> -m \"Initial Import\" svn
checkout <file:///full/path/to/dir> workingtestdir

svn status

from working dir

svn commit -m \"comment\"

update working copy with the data in the repo

svn update

<http://blog.circlesixdesign.com/2007/04/12/svn-getting-started-2/>
