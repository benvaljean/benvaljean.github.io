---
layout: post 
title: Vim
---

Vi is free, open-source advanced text editor. A clone of Vi called
[Vim](http://www.vim.org) is now commonly used as a *vImproved*
alternative. It is often used on Linux flavours although ports for
Windows [gVim portable](http://portablegvim.sourceforge.net/) and Mac
OSX [Vim for Mac](http://macvim.org/OSX/index.php) are available. It has
many keyboard-shortcut-based commands, just a few of which are listed
here.

### Commands

#### Movement

##### Command mode

Beginning of word: **b**\
End of current word: **e**\
Beginning of line: **0** or **\^**\
End of line: **\$**\
====Insert mode==== Beginning of line: Home key\
End of line: End key

#### Search and replace

    :%s/OLD/NEW/g

#### Delete all occurances of a string

    :g/STRING/d

#### Delete all empty lines

    :g/^$/d

#### Delete all lines with only spaces

    :g/^ *$/d

#### Delete all duplicate lines

    :sort u

#### Jump to beginning / end of file

\'G\' alone moves the cursor to the end of file; \'gg\' to the beginning
of the file.

#### Show line numbers

    :set number

#### Hide line numbers

    :set nonumber

#### Goto line number 20

    :20

#### Cut/Delete a whole line

To cut the current line:

    dd

To cut 10 lines below the cursor:

    10dd

#### Copy/Yank many lines

To copy the current line:

    Y

To copy 10 lines below the cursor:

    10Y

To copy all lines below the curosr:

    yG

#### Paste a whole line

The data from this line is placed in a local clipboard called a register
and can be restored with \'p\' (below cursor) or \'P\' (above cursor).

#### Insert text at the beginning on each line

Insert a double quote `"` at the beginning of each line:

    :%s!^!"!

#### Insert text at the beginning of all lines below the cursor

Useful for commenting out text in bulk in Apache, insert a `#` at the
beginning of all ines below the cursor:

    :.,$s!^!#!

`.` means current line\
`,` range delimeter\
`$` refers to EOF/last line\
`s` substitute command\

#### Show Clipboard items / registers

    :reg

#### Paste from register number 2

    "2p

#### Allow pasting in Vi without Indents

    :set paste

#### Create a new line below the current line

    o

#### Append text at the end of the current line

    A

#### Delete trailing white space form all lines

    :%s/\\s\\+$//

#### Visual mode commands

Whilst in command mode, press **v** to enter visual mode. The cursor
keys can now be used to select text. the following commands will affect
the text that has been selected. Copy/Yank and Cut/Delete can also be
used with visual mode.

###### Indent text

    >

###### De-Indent text

    <

###### Sort text

*To pipe any selected text into an external command and replace with its
output*:

    :! command

Use sort:

    :! sort

#### Using external commands

Vim can run an external command with the current file. The file saved on
disk or the current unsaved buffer can be used:\
`%` File on disk\
`-` Current buffer

###### Diff current unsaved buffer with saved version

    :w !diff % -

###### Get number of lines through wc

    :w !wc -

###### Syntax check of PHP

    :w !php5 -l -

###### Recall previous external command

*Same as Bash:* `:!!`

###### Insert command output

    :r !echo hello

#### Cheat sheet

<http://www.eec.com/business/vi.html>

### Settings commands by default

If a particular option or command needs to be the default in Vim - it
needs to be run every time you start Vim - create a text file called
`.exrc` or `.vimrc` in your home directory and place your commands in
there without the proceeding colon. For example to display line numbers
and search case insensitively by default your .vimrc file would look
like this:

    set number
    set ignorecase

### Viewing panes

To split the current file into two horizontal panes:

    :split

Use Ctrl+W to switch panes.

### Recall previous command

Press Esc to enter command mode, type a single colon, after which the up
and down keys can be used in the same manner as BASH.

### Redo last typed text

Type a set of text in INSERT mode and go into COMMAND mode by pressing
Esc. Now pressing `.` (a dot/period) will re-type the text typed in.

### Tabs

Vim can open many files at once and arrange them in tabs:

    vim -p blah.csv blah2.csv

To move between tabs use `:tabn` and `:tabp`

#### Run a command on all files/tabs open

     :tabdo $s/replace/this/g

### See Also

[Regular Expressions](Regular_Expressions "wikilink")

[Category:Linux](Category:Linux "wikilink")
