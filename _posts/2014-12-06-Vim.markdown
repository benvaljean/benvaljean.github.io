---
layout: post 
title: Vim
---

### Commands

#### Search and replace

    :%s/OLD/NEW/g

#### Go to line nunber

<linenumber>G

\'G\' alone moves the cursor to the end of file; \'gg\' to the beginning
of the file.

#### Show line numbers

    :set number

#### Hide line numbers

    :set nonumber

#### Goto line number 20

    :20

#### Cut/Delete a whole line

    dd

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

#### Cheat sheet

<http://www.eec.com/business/vi.html>
