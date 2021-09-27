---
layout: post 
title: Rename file for all previous commits in Git
tags: Git
---

Renaming a file for all previous, historical commits can be done using two approaches. Unless your file contains a `:` it is best to use `git filter-repo`, otherwise `git filter-branch` can be used.

### Using git filter-repo

    git filter-repo --path-rename full/path/to/file.old:full/path/to/file.new


Path-rename does not work if the current dir is not in the repo root. For instance in the example above the following does **not** work:

    # Does not work!
    cd full/path/to/
    git filter-repo --path-rename file.old:file.new


### Using filter-branch

Filter branch is slower and has a number of problems, but if you need to use it:

    git filter-branch --tree-filter '
    if [ -f full/path/to/file.old ]; then
    mv full/path/to/file.old full/path/to/file.new
    fi' --force HEAD




