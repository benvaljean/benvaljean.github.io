---
layout: post 
title: Bash Scripting
---

BASH [http://www.gnu.org/software/bash/ (Bourne Again Shell)] is a command shell and interpretor for Linux.

==Parameters==
$#  Number of parameters

$1  First parameter

$0  Name of the script

$@  All the parameters in one string
==Get IP address==

The following command will print the IP address by itself allowing you to pipe it into a command or an environment variable:
<pre>ifconfig|grep "inet addr:"|grep -v "127.0.0.1"|cut -d: -f2|awk '{ print $1}'</pre>

==Loops==
===Iterate through words in a string===
<pre>
users="tom jerry ben"
for character in $users
do
  echo $character is a good name
done
</pre>
===Looping through a series of numbers===
<pre>
for i in `seq 1 5`;
do
  echo $i
done
</pre>

==If==
<pre>
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
</pre>
===Numeric Operators===
====Single Braces====
{| {{table}}
| -eq||equal
|-
| -ne||not equal
|-
| -gt||greater than
|-
| -ge||greater than or equal to
|-
| -lt||less than
|-
| -le||less than or equal to
|}
====Double Parentheses====
Standard mathematical operators apply
{| {{table}}
| <=||less than or equal to
|-
| >||greater than
|-
| >=||greater than or equal to
|}
===String Operators===
====Single Braces====
{| {{table}}
| =||equal
|-
| ==||equal, but has file globbing and word splitting when wildcarded without quotes, and literal matching with quotes
|-
| !=||not equal
|-
| -z||string is null
|-
| -n||string is not null - MUST be quoted string but string should always be quoted anyway...
|}
====Double Braces====
{| {{table}}
| <||less than in ASCII order
|-
| >||more than in ASCII order
|-
| ==||equal, but has pattern matching when wildcarded, literal matching with quotes
|}
===Test if number===
<pre>
[[ "$var" =~ ^[0-9]+([.][0-9]+)?$ ]] && echo $var is a number
</pre>

==Force run as root==
<pre>
if [ $UID != "0" ];then echo Only root can run this command 1>&2;exit 1;fi
</pre>

==Favorite Resources==
[http://books.google.co.uk/books?hl=en&id=OztsPBFGhDIC&dq=BASH&printsec=frontcover&source=web&ots=p_MixNXpzD&sig=9y_nSRxEbj9jU4HJUMsAO7l-3Y0 BASH for beginners book]<br>
[http://www.thelinuxblog.com/bash-scripting-techniques/ BASH Scripting Techniques]<br>
[http://steve-parker.org/sh/buy/shellscriptingbook-sample.pdf Steve Parker's Shell Scrpting Book]<br>
[http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html If]<br>
[http://tldp.org/LDP/abs/html/refcards.html Operators and constructs]

[[Category:Linux]][[Category:Bash]]
