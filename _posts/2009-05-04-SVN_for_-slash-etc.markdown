---
layout: post 
title: SVN for /etc
---

[Subversion](http://subversion.tigris.org/) also known as SVN is a
version control system. Normally users \'checkout\' data from a central
repository to a local \'working copy\'. However it can be setup to allow
version control for files /etc .

### Installation

    sudo svnadmin create /svn
    sudo chmod -R go-rwx /svn/
    sudo svn mkdir file:///svn/etc -m"creating empty dir for svn"
    cd /etc
    sudo svn checkout file:///svn/etc .
    sudo rm -R .svn/
    sudo svn checkout file:///svn/etc .
    sudo svn add *
    sudo svn commit -m"initial commit of /etc"

This creates an SVN repository /svn/etc with the working copy being /etc
itself. Edit files as would be done normally and \'commit\' them to the
repository to allow them to be version-controlled:

    sudo svn commit file

To revert a file back to a previous revision for instance:

    sudo svn update -r 2 hosts

### See Also

<http://ariejan.net/2007/07/04/how-to-resolve-subversion-conflicts/>

<http://svnbook.red-bean.com/en/1.2/svn.branchmerge.commonuses.html#svn.branchmerge.commonuses.undo>

[Category:Linux](Category:Linux "wikilink")
