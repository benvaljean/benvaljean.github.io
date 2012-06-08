---
layout: post 
title: Getting started with GIT
---

[GIT](http://git-scm.com) is a relatively new Version Control System\]

#### Create new repo

Cd to the dir where version tracking is required and create the repo:

    git init

Version track \*.sh and \*.pl files:

    git add *.pl
    git add *.sh

Perform your first commit:

    git commit -m "Initial commit"

Re-commit every time changes are made:

    git commit -a -m "test1"

#### Reverting a commit

Use `git log` to view the list of commits, note the long alpha-numeric
after \"commit\".

    git revert <commit-number>

#### Setup remote repo

Setup a bare remote repo:

    ssh remote-server
    mkdir -p /var/git/repo1
    cd /var/git/repo1
    git --bare init
    exit

In your new repo folder:

    git remote add origin ssh://remote-server/var/git/repo1

The following command will now push your repo to remote-server:

    git push origin master

#### Clone an existing repo

Note that the term \'check-out\' is specifically not used here, as
\'check out\' in GIT is completely different to \'check-out\' in
CVS/SVN. A check-out in CVS/SVN is called \'clone\' in GIT.

    git glone http://blah.com/repos/bgrepo.git

Repos can also be setup using GITs own protocol in the form of
`git clone `[`git://`](git://)`...` or over SSH as described above or
with `git clone user@host:repos/bgrepo.git`

#### Making stages

GIT unlike CVS/SVN has a \'staging\' principal. Changes that are made to
files in your local repo are not automatically committed when
`git commit` is run. All local changes must be set to be \'ready to
commit\' instead, which is is called \'staging\' in SVN-speak. This is
done from the `git add` which is also used to add files to the repo as
in CVS/SVN. Local changes made since `git add` was run will NOT be
committed! Instead the changes up to the last time `git add` was run on
the file are committed. This is an important point as this is very
different to the principals behind CVS/SVN and indeed other VCS.

It is possible to force git to place all local changes into staging
before the commit ala CVS/SVN with the `-a` argument. This will place
into staging files which already tracked - `git add` is only required to
add new tracked files to the repo.

#### Renaming files

GIT does not automatically track file renames, however if a file is
removed and re-added to the repo the change history is still retained.

-   Both of these commands have the same result:

<!-- -->

    git mv script.pl script2.pl

    mv script.pl script2.pl
    git rm script.pl
    git add script2.pl

#### References

<http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository>
