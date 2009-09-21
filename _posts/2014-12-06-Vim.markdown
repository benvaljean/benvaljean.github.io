---
layout: post 
title: Vim
---

Vi is free, open-source advanced text editor. A clone of Vi called
[Vim](http://www.vim.org) is now commonly used as a *vImproved*
alternative. It is often used on Linux flavours although ports for
Windows [gVim portable](http://portablegvim.sourceforge.net/) and Mac
OSX [Vim for Mac](http://macvim.org/OSX/index.php) are available. Its
differentiator from other text editors is the many
keyboard-shortcut-based commands available, just a few of which are
listed here.

### Commands

#### Search and replace

    :%s/OLD/NEW/g

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

The data from this line is placed in a local clipboard and can be
restored with \'p\' (below cursor) or \'P\' (above cursor).

#### Allow pasting in Vi without Indents

On earlier distributions pasting in Vi from the OS can be tricky as
indents are placed on the lines. To disable this:

    :set paste

#### Create a new line below the current line

    o

#### Cheat sheet

<http://www.eec.com/business/vi.html>

### Recall previous command

Press Esc to entewr command mode, type a single colon, after which the
up and down keys can be used in the same manner as BASH.

[Category:Linux](Category:Linux "wikilink")
