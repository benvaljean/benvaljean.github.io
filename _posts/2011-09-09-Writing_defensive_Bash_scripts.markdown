---
layout: post 
title: Writing defensive Bash scripts
---

Any kind of script should be written to expect the unexpected, this is known as programming ''defensively''.

===Exit on error===
<pre>set -o errexit</pre>
The script will exit if any statement returns a non-zero exit code. Ensure that no statement or command returns a non-zero exit code as part of its normal operation as this option could cause the script to break where it might otherwise have worked.
===Exit on use of missing variable===
<pre>set -o nounset</pre>
The script will exit if any statement attempts to refer to a missing variable. Commands can have very-undesired affects if a variable returns, consider <tt>rm -Rf $var/etc/apache2</tt>. 
====Using $?====
The <tt>$?</tt> environment variable will not work if <tt>set -o errexit</tt> is set as BASH will exit on the line before. The following can be used as an alternative:
<pre>
/bin/command || { echo "error";exit 1; }</pre>
===Expect for files to be missing===
<pre>
mkdir -p /path/to/dir
rm -f file</pre>
Create parent folders if they do not exist and do not return a non-zero value if files do not exist with rm.
===Always use quotes around variables===
Otherwise a space will cause statements using it fail usually.
===Be prepared for the script to be killed or otherwise exit early===
The <tt>trap</tt> command allows a command or sub to be run upon the script receiving a signal. There are many signals that can be ''trapped'' but three most useful are:
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Signal'''
| align="center" style="background:#f0f0f0;"|'''Case'''
|-
| INT||Interupt - user presses Ctrl+C
|-
| TERM||Terminate - user kills the script using kill
|-
| EXIT||Triggered when the script exits normally or from a condition using the set command.
|}
To clear up temp files upon exiting normally or abnormally:
<pre>
trap "rm -f /tmp/file; exit" INT TERM EXIT
command1
command2
trap - INT TERM EXIT
</pre>
Different traps can be configured by specifiying the signals in separate commands.

[[Category:Linux]][[Category:Bash]]
