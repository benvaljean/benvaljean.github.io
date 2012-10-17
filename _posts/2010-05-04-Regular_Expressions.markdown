---
layout: post 
title: Regular Expressions
---

Regular expressions and used in [[Perl]], [[Apache Rewrite]], [[Vim]] among many other uses.

{| {{table}}
| align="center" style="background:#f0f0f0;"|'''Regex'''
| align="center" style="background:#f0f0f0;"|'''Meaning'''
|-
| .|| Any single character except a newline
|-
| ^|| The beginning of the line or string
|-
| $|| The end of the line or string
|-
| *|| Zero or more of the last character
|-
| +|| One or more of the last character
|-
| ?|| Zero or one of the last character
|-
| (ben\\.)?goodacre.name|| ben.goodacre.name or goodacre.name
|-
| t.e|| t followed by any 1 single character followed by e.  This will match <tt>the</tt> , <tt>tre</tt> , <tt>tle</tt> , but not <tt>te</tt> or <tt>tale</tt>
|-
| ^f|| f at the beginning of a line
|-
| ^ftp|| ftp at the beginning of a line
|-
| e$|| e at the end of a line
|-
| und*|| un followed by zero or more d characters. This will match <tt>un</tt> , <tt>und</tt> , <tt>undd</tt> , <tt>unddd</tt> etc.
|-
| .*|| Any string without a newline. This is because the . matches anything except a newline and the * means zero or more of these.
|-
| ^$|| A line with nothing in it.
|-
| [qjk]||Either q or j or k
|-
| [^qjk]||Neither q nor j nor k
|-
| [a-z]||Anything from a to z inclusive
|-
| [^a-z]||No lower case letters
|-
| [a-zA-Z]||Any letter
|-
| [a-z]+||Any non-zero sequence of lower case letters
|-
| [^qjk]+ ||Any non-zero sequence that does not contain a q nor j nor k. 
|-
| jelly<nowiki>|</nowiki>cream||Either jelly or cream
|-
| (eg|le)gs||Either eggs or legs
|-
| (da)+||Either da or dada or dadada or...
|-
| \
||A newline
|-
| \    ||A tab
|-
| \\w||Any alphanumeric (word) character.
|-
| ||The same as [a-zA-Z0-9_]
|-
| \\W||Any non-word character.
|-
| ||The same as [^a-zA-Z0-9_]
|-
| \\d||Any digit. The same as [0-9]
|-
| \\D||Any non-digit. The same as [^0-9]
|-
| \\s||Any whitespace character: space, tab, newline, etc
|-
| \\S||Any non-whitespace character
|-
| \\b||A word boundary, outside [] only
|-
| \\B||No word boundary
|}
===Match a date yyyy-mm-dd===
<pre>\\d{4}-\\d{2}-\\d{2}</pre>
Needs some work, will also match 9999-99-99 .
===Time hh:mm:ss===
<pre>\\d{2}:\\d{2}:\\d{2}</pre>
Needs some work, will also match 99:99:99 .
===Mac address===
With -'s or :'s
<pre>
[0-9a-f][0-9a-f][:-][0-9a-f][0-9a-f][:-][0-9a-f][0-9a-f][:-][0-9a-f][0-9a-f][:-][0-9a-f][0-9a-f][:-][0-9a-f][0-9a-f]
</pre>
===IP adress===
<pre>^([0-9]|[1-9][0-9]|1([0-9][0-9])|2([0-4][0-9]|5[0-5]))\\.([0-9]|[1-9][0-9]|1([0-9][0-9])|2([0-4][0-9]|5[0-5]))\\.([0-9]|[1-9][0-9]|1([0-9][0-9])|2([0-4][0-9]|5[0-5]))\\.([0-9]|[1-9][0-9]|1([0-9][0-9])|2([0-4][0-9]|5[0-5]))$</pre>
''References http://www.analyticsmarket.com/freetools/ipregex''
