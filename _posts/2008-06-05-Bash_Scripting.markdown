---
layout: post 
title: Bash Scripting
---

BASH [(Bourne Again Shell)](http://www.gnu.org/software/bash/) is a
command shell for Linux as DOS/Command prompt is to Windows.

### Get IP address

The following command will print the IP address by itself allowing you
to pipe it into a command or an environment variable:

    ifconfig|grep "inet addr:"|grep -v "127.0.0.1"|cut -d: -f2|awk '{ print $1}'

### Simple loop

    users="tom jerry ben"
    for character in $users
    do
      echo $character is a good name
    done

### Simple If

    oldusers="tom jerry sam micky minnie"
    if [ ! -d /var/spool/mail ]; then
            echo /var/spool/mail not found - check location
    else
            echo Checking /var/spool/mail
            for user in $oldusers
            do
            if [ -e /var/spool/mail/$user ]; then
                    echo /var/spool/mail/$user exists
            fi
    fi

### Favorite Resources

[BASH for beginners
book](http://books.google.co.uk/books?hl=en&id=OztsPBFGhDIC&dq=BASH&printsec=frontcover&source=web&ots=p_MixNXpzD&sig=9y_nSRxEbj9jU4HJUMsAO7l-3Y0)\
[BASH Scripting
Techniques](http://www.thelinuxblog.com/bash-scripting-techniques/)\
[Steve Parker\'s Shell Scrpting
Book](http://steve-parker.org/sh/buy/shellscriptingbook-sample.pdf)

[Category:Linux](Category:Linux "wikilink")
