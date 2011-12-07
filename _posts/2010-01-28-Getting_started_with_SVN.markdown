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

### Setup new repo

    $ mkdir new-repo
    $ svnadmin create new-repo

Add users to new-repo/conf/passwd:

    [users]
    user = plaintextpass

Setup permissions in new-repo/conf/authz:

    [groups]
    new-repo_rw = user,user2

    [/]
    @new-repo_rw = rw

<http://blog.circlesixdesign.com/2007/04/12/svn-getting-started-2/>
