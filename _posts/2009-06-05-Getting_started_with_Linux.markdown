---
layout: post 
title: Getting started with Linux
---

Copy all files inc subdirs:

    cp -a /usr/local/foo/* /var/temp/bar

Delete all files inc subdirs:

    rm -rf folder

Find files with indexer:

    updatedb
    locate filename

Find files without indexer:

    find /dir -name filename
    find /dir -name '*part of file name*'

Search for packages that contain a certain file

    apt-file search filename

Delete everything older than 7 days:

    find /directoryname -type f -mtime +7 -exec rm {} \\;

Search text within files and print the lines:

    find /dir -type f -exec grep "textinfile" {} \\;

Search text within files and print only the filenames:

    find /dir -type f | xargs grep -li "textinfile"

Search and replace over multiple files:

    perl -pi -w -e 's/old/new/g;' *.php

Show listening ports and the processes using the ports:

    sudo netstat -anp|grep LIST

Show processes sorted by memory usage descending:

    ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS

Strip out characters from text:

    ;Strip colons from a MAC address
    echo 00:00:00:00:00:00 | tr -d ':'
    000000000000

Ascertain what line in the rouitng table a particular destination ip
uses:

    /sbin/ip ro get 1.1.1.1

Setup a portable prompt with user\@host: pwd on systems that have an old
prompt by default, like some BSD machines

    PS1='\\u@\\h:\\w\\$'

Case-insensitive search in less: *or type -i*

    /normal search text here/i

Delete the first character of every line:

    cat file|sed 's/^.//'

Redirect standard output and standard error to a file:

    command >file 2>&1

Pipe standard output and standard error: *tee in this example*

    script 2>&1 | tee file

Show files accessed this year:

    ls -Rlua /dir|grep -v '\\.$'|grep `date "+%Y"`

Add to bashrc for a `scpnewestfile user@host:/dir` command to
automatically scp the most recen tly modified file to another host:

    scpnewestfile()
    {
    scp `ls -ltr|tail -1|cut -d ' ' -f8` $1
    }

Du for each folder without showing subdirs:

    for i in `find . -maxdepth 1 -type d`; do du -sh $i; done;

SSH Auto complete:

    SSH_COMPLETE=( $(cat ~/.ssh/known_hosts | \\
                     cut -f 1 -d ' ' | \\
                     sed -e s/,.*//g | \\
                     uniq | \\
                     egrep -v [0123456789]) )
    complete -o default -W "${SSH_COMPLETE[*]}" ssh

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

Find words in garbled text [^2]

    echo "Garbled Text" | grep -o -F -f /usr/share/dict/words | sed -e "/^.$/d"

### References

<references/>

[Category:Linux](Category:Linux "wikilink")

[^1]: <http://www.shell-fu.org/lister.php?id=553>

[^2]: <http://www.shell-fu.org/lister.php?id=525>
