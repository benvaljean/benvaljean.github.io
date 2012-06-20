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
    svn co file:///full/path/to/dir workingtestdir

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

Commit changes to repo:

    svn ci file

View changes between revisions

    svn diff -r10:12

View changed files only

    svn diff --summarize -r10:12 http://svn.example.com/trunk

#### References

<http://www.learnosity.com/techblog/index.cfm/2009/1/16/SVN--Get-list-of-files-changed-between-revisions>

[Category:Linux](Category:Linux "wikilink")
