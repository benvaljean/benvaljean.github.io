---
layout: post 
title: Getting started with SVN
---

### Setup new repo

    mkdir new-repo
    svnadmin create new-repo
    mkdir test
    touch test/test1.txt
    touch test/test2.txt
    svn import dir file:///full/path/to/dir -m "Initial Import"
    svn checkout file:///full/path/to/dir workingtestdir

Add users to new-repo/conf/passwd:

    [users]
    user = plaintextpass

Setup permissions in new-repo/conf/authz:

    [groups]
    new-repo_rw = user,user2

    [/]
    @new-repo_rw = rw

Update working copy with data from repo

    svn update

[Category:Linux](Category:Linux "wikilink")
