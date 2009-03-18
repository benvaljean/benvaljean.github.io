---
layout: post 
title: Automated rsync for backup
---

For the purpises of this page backups are being done from \'liveserver\'
to \'backupserver\'

Create key on liveserver:

ssh-keygen -t dsa -b 2048 -f /root/rsync.key

Do not type in a pass

Cat the rsync.key.pub file that is created into
//backupserver/root/.ssh/authorized\_keys

You should then be albe to ssh root\@backupserver from liveserver
without requiring a pass, if it still asks for pass use the -i param to
force it to use the key.

Create a new file in /etc/cron.d to run the backup, the following runs a
mysql backup every day at 2am and then rsyncs it to the backup server
every day at 5am:

    0 2 * * * root /usr/local/bin/automysqlbackup.sh
    0       5       *       *       *       root    /usr/bin/rsync -azue "ssh -i /root/rsync.key" /var/backup/mysql backupserver:/backups/mysql/wiki_intranet

thats it!
