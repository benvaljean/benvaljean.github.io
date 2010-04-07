---
layout: post 
title: Getting started with Linux
---

Copy all files inc subdirs:<pre>cp -a /usr/local/foo/* /var/temp/bar</pre>
Delete all files inc subdirs:<pre>rm -rf folder</pre>
Find files with indexer:
<pre>
updatedb
locate filename
</pre>
Find files without indexer:
<pre>
find /dir -name filename
find /dir -name '*part of file name*'
</pre> 
Search for packages that contain a certain file
<pre>
apt-file search filename</pre>
Delete everything older than 7 days:<pre>
find /directoryname -type f -mtime +7 -exec rm {} \\;</pre>
Search text within files and print the lines:<pre>
find /dir -type f -exec grep "textinfile" {} \\;
</pre>
Search text within files and print only the filenames:
<pre>find /dir -type f | xargs grep -li "textinfile"</pre>
Search and replace over multiple files:
<pre>perl -pi -w -e 's/old/new/g;' *.php</pre>
Show listening ports and the processes using the ports:
<pre>sudo netstat -anp|grep LIST</pre>
Show processes sorted by memory usage descending:
<pre>ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS</pre>
Strip out characters from text:
<pre>
;Strip colons from a MAC address
echo 00:00:00:00:00:00 | tr -d ':'
000000000000
</pre>
Ascertain what line in the rouitng table a particular destination ip uses:
<pre>/sbin/ip ro get 1.1.1.1</pre>
Setup a portable prompt with user@host: pwd on systems that have an old prompt by default, like some BSD machines
<pre>PS1='\\u@\\h:\\w\\$'</pre>
Case-insensitive search in less:  '''or type -i'''<pre>/normal search text here/i
[[Category:Linux]]
