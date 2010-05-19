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
| t.e|| t followed by anthing followed by e
|-
| || This will match <tt>the</tt> , <tt>tre</tt> , <tt>tle</tt> , but not <tt>te</tt> or <tt>tale</tt>
|-
| ^f|| f at the beginning of a line
|-
| ^ftp|| ftp at the beginning of a line
|-
| e$|| e at the end of a line
|-
| tle$|| tle at the end of a line
|-
| und*|| un followed by zero or more d characters
|-
| || This will match <tt>un</tt> , <tt>und</tt> , <tt>undd</tt> , <tt>unddd</tt> etc.
|-
| .*|| Any string without a newline. This is because the . matches anything except a newline and the * means zero or more of these.
|-
| ^$|| A line with nothing in it.
|-
| 
|-
| [qjk]||Either q or j or k
|-
| [^qjk]||Neither q nor j nor k
|-
| [a-z]||Anything from a to z inclusive
|-
| [^a-z]||No lower case letters
|-
| [a-zA-Z]Any letter
|-
| [a-z]+||Any non-zero sequence of lower case letters
|-
| 
|-
| jelly|cream||Either jelly or cream
|-
| (eg|le)gs||Either eggs or legs
|-
| (da)+||Either da or dada or dadada or...
|-
| 
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
