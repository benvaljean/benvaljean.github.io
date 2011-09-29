---
layout: post 
title: Bash Tricks
---

===Keyboard Shortcuts===
{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Ctrl + A'''
| align="center" style="background:#f0f0f0;"|'''Go tobeginning of line'''
|-
| Shortcut||Function
|-
| Ctrl + E||Go to end of line
|-
| Ctrl + U||Clear all characters to the left of the cursor
|-
| Ctrl + R ||Search through command history
|-
| Ctrl + C||Kill whatever you are running
|-
| Ctrl + Z||Background current process. <tt>fg</tt> restores it.
|-
| Ctrl + W||Delete the word before the cursor
|-
| Ctrl + K||Clear all characters to the right of the cursor
|-
| Esc + T||Swap the last two words before the cursor
|-
| Alt + F||Move cursor forward one word on the current line
|-
| Alt + B||Move cursor backward one word on the current line
|-
| Alt + .||Cycle through arguments used in previous commands
| 
|}
===Redirecting Output===
Redireting output in many cases is as simple as UNIX/DOS:
<pre>find ~ -name test >outputfile</pre>
This will only redirect the standard output, to redirect standard error:
<pre> find ~ -name test 2>erroroutputfile</pre>
To redirect the output of both standard output AND standard error:
<pre>find ~ -name test >outputwitherrorsfile 2>&1</pre>

===Eliminate 'loser takes all' Bash History===
Bash only writes the command history on exiting the shell. If multiple sessions are open simultaneously the very last session to be closed will overwrite any command history from other sessions since it was opened. Confused? try the following:
#Opening a shell and type <tt>echo 1;echo 2</tt> (session number 1.)
#Keep this session open and open another bash session (session number 2) and use the <tt>history</tt> command and you will see that the last two commands issued are not there, as the commands are only written on exiting the shell. But that it not all...
#Close session 1 and reopen another session (session number 3) and you will now see the <tt>echo 1;echo 2</tt>
#Close session number 2 and reopen another session (session number 4) and you will now see that <tt>echo 1;echo 2</tt> has been lost!
====How to fix====
#Bash to save to the history upon every command, not when the session exits
#Bash must always append instead of overwriting command history.
#The <tt>history</tt> command must re-read the newlines upon running it, by default it only reads it when the session is started.


*Add the following to .bashrc:
<pre>
PROMPT_COMMAND='history -a'
shopt -s histappend
alias history='history -n;history'
</pre>

===Refer to previous dirs and commands===

Refer to the last dir within a command with: <pre>~-/</pre>
Insert the last command entered with: <pre>!!</pre> If, for example sudo is not used when it should have been <tt>sudo !!</tt> can be used as an alternative to retyping/copying/pasting the last command.
<p>Insert all the arguments from the previous command with <pre>!*</pre></p>
Refer to the Nth argument of the last command:<pre>!!:n</pre>
Refer to the first argument:<pre>!!:2</pre>
Refer to the last argument:<pre>!:$</pre>

===Dir navigation===
cd with no arguments always goes to your home dir.<br>
cd to last dir: <tt>cd -</tt><br>
Put current dir in the stack <tt>pushd .</tt>      Then go back to it with <tt>popd</tt><br>
Go to dir, run a command and then return to the current dir: <tt>(cd dir && command)</tt>

===Scrolling ls listings made easier===
Instead of  <tt>ls /etc|less</tt>  this can be shortened to  <tt>less /etc</tt>  . If a folder is specified in less it will <tt>ls</tt> is and <tt>less</tt> the contents.
===Simple calculator===
Only useful as a simple calculator as an alternative to using a full caclualator like <pre>bc -l</pre>; fractions are decimals are not supported:
<pre>
$ echo $[16*2]
32
$ echo $[100/11]
9
</pre>

==See Also==
*[http://www.gnu.org/software/bash/manual/html_node/index.html Bash Reference Manual]
*[http://www.linuxjournal.com/article/7385 My Favorite bash Tips and Tricks]
*[http://www.ukuug.org/events/linux2003/papers/bash_tips/ Bash Tips & Tricks  - Simon Myers - UKUUG Linux 2003 Conference • August 2003]
*[http://twitter.com/bashtips Bashtips on twitter]
*[http://www.catonmat.net/blog/the-definitive-guide-to-bash-command-line-history The Definitive Guide to Bash Command Line History]

[[Category:Linux]]
