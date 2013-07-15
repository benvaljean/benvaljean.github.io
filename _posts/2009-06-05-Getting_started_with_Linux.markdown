---
layout: post 
title: Getting started with Linux
---

#### File searching/manipulation

Copy all files inc subdirs:

    cp -a /usr/local/foo/* /var/temp/bar

Delete all files inc subdirs:

    rm -rf folder

SCP a folder including sub-dirs:

    scp -r folder/ 1.1.1.1:

Find files with indexer:

    updatedb
    locate filename

Find files without indexer:

    find /dir -name filename
    find /dir -name '*part of file name*'

Delete everything older than 7 days:

    find /directoryname -type f -mtime +7 -exec rm {} \\;

Search text within files and print the lines:

    find /dir -type f -exec grep "textinfile" {} \\;

Search text within files and print only the filenames:

    find /dir -type f | xargs grep -li "textinfile"

Search and replace over multiple files:

    perl -pi -w -e 's/old/new/g;' *.php

Show files accessed this year:

    ls -Rlua /dir|grep -v '\\.$'|grep `date "+%Y"`

Du for each folder without showing subdirs:

    for i in `find . -maxdepth 1 -type d`; do du -sh $i; done;

Remove duplicate files [^1] The script below will find duplicate files
(files with the same md5sum) in a specified directory and output a new
shell script containing commented-out rm statements for deleting them.
You can then edit this output to decide which to keep.

    OUTF=rem-duplicates.sh;
    echo "#! /bin/sh" > $OUTF;
    find "$@" -type f -print0 |
      xargs -0 -n1 md5sum |
        sort --key=1,32 | uniq -w 32 -d --all-repeated=separate |
        sed -r 's/^[0-9a-f]*( )*//;s/([^a-zA-Z0-9./_-])/\\\\\\1/g;s/(.+)/#rm \\1/' >> $OUTF;
    chmod a+x $OUTF; ls -l $OUTF

#### Networking

Show listening ports and the processes using the ports:

    sudo netstat -ltnup

Ascertain what line in the rouitng table a particular destination ip
uses:

    /sbin/ip ro get 1.1.1.1

View routing table:

    route -n

Add static route:

    sudo ip route add networkaddress/cidr via next_hop_ip

#### Investigating a system / Troubleshooting

*See also [Linux System
Troubleshooting](Linux_System_Troubleshooting "wikilink")*\
Show processes sorted by memory usage descending:

    ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS

#### Text Manipulation

Strip out a single character from text:

    ;Strip colons from a MAC address, tr cannot be used when stripping a phrase
    echo 00:00:00:00:00:00 | tr -d ':'
    000000000000

Strip out the phrase \'remove me\' from text:

    cat file|sed '/s/remove me//g'

Delete the first character of every line:

    cat file|sed 's/^.//'

Find words in garbled text [^2]

    echo "Garbled Text" | grep -o -F -f /usr/share/dict/words | sed -e "/^.$/d"

Get columns 1 and 3 and seperate with commas:

    cat file | awk -v OFS=',' '{print $1, $3}'

#### BASH

*See Also [BASH Tricks](BASH_Tricks "wikilink")*\
Setup a portable prompt with user\@host: pwd on systems that have an old
prompt by default, like some BSD machines

    PS1='\\u@\\h:\\w\\$ '

Add to bashrc for a `scpnewestfile user@host:/dir` command to
automatically scp the most recently modified file to another host:

    scpnewestfile()
    {
    scp `ls -ltr|tail -1|tr -s ' '|cut -d ' ' -f8` $1
    }

#### Archiving

Create tar archive

    tar -cvzf files.tar.gz file1 file2 file3 filen

Create bz2 archive of dir/

    tar -c dir/ | bzip2 > dir.tar.bz2

Extract archive

    bzip2 -dc dir.tar.bz2|tar -x

Copy dir/ with permissions to remote machine

    ( tar -c /dir/to/copy ) | ssh -C user@remote 'cd /where/to/ && tar -x -p'

#### Less

*See Also: [Less Tricks](Less_Tricks "wikilink")*\
Case-insensitive search in less: *or type -i*

    /normal search text here/i

#### Redirecting Output

Redirect standard output and standard error to a file:

    command >file 2>&1

Pipe standard output and standard error: *tee in this example*

    script 2>&1 | tee file

#### SSH

SSH Auto complete:

    SSH_COMPLETE=( $(cat ~/.ssh/known_hosts | \\
                     cut -f 1 -d ' ' | \\
                     sed -e s/,.*//g | \\
                     uniq | \\
                     egrep -v [0123456789]) )
    complete -o default -W "${SSH_COMPLETE[*]}" ssh

#### RPM

Query all installed packages, similar to `yum list installed`

    rpm -qa

Query package owning a file

    rpm -qf /bin/file

List files installed by a package

    rpm -qc package

List status of files installed by a package [^3]

    rpm -qs package

List post install and uninstall scripts inside an rpm [^4]

    rpm --scripts -qp package.rpm

#### Aptitude

Search for packages of a given name or description:

    apt-cache search virtualbox

Search for packages that contain a certain file

    apt-file search filename

##### Auto install security updates (Ubuntu)

Package unattended-upgrades allows this - installed by default but not
automatically scheduled to run by default.

Install security updates only:

    sudo unattended-upgrade

Configure to download/install security updates automatically, excluding
any that have additional dependancies:

    sudo dpkg-reconfigure -plow unattended-upgrades

See Also: /usr/share/doc/unattended-upgrades/README

#### Misc

Stopwatch on your linux machine: `time cat` to srart, Ctrl+D to stop\
Show startup items:`chkconfig --list`

### References

<references/>

[Category:Linux](Category:Linux "wikilink")

[^1]: <http://www.shell-fu.org/lister.php?id=553>

[^2]: <http://www.shell-fu.org/lister.php?id=525>

[^3]: <http://www.rpm.org/max-rpm/s1-rpm-query-parts.html>

[^4]: <http://www.linuxquestions.org/questions/programming-9/how-to-extract-spec-file-from-rpm-file-426847/>
