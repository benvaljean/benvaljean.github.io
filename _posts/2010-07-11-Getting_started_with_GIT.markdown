---
layout: post 
title: Getting started with GIT
---

Cd to the dir where version tracking is required and creator the repo:

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
    ===Setup remote repo===
    Setup a bare remote repo:
    <pre>ssh remote-server
    mkdir -p /var/git/repo1
    cd /var/git/repo1
    git --bare init
    exit

In your new repo folder:

    git remote add origin ssh://remote-server/var/git/repo1

The following command will now push your repo to remote-server:

    git push origin master
