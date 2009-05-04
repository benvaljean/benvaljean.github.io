---
layout: post 
title: SVN for /etc
---

      604  s svnadmin create /svn
      605  s chmod -R go-rwx /svn/
      606  svn mkdir file:///svn/etc -m"creating empty dir for svn"
      607  s svn mkdir file:///svn/etc -m"creating empty dir for svn"
      608  cd /etc
      609  s svn checkout file:///svn/etc .
      610  s rm -R .svn/
      611  s svn checkout file:///svn/etc .
      612  s svn add *
      613  s svn commit -m"initial commit of /etc"

This creates an SVN repository /svn/etc with the working copy being /etc
itself. Edit files as would be done normally and \'commit\' them to the
repository to allow them to be version-controlled:

    s svn commit file

To revert a file back to a previous revision for instance:

    s svn update -r 2 hosts

<http://ariejan.net/2007/07/04/how-to-resolve-subversion-conflicts/>
