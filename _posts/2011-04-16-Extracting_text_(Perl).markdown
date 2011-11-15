---
layout: post 
title: Extracting text (Perl)
---

The `split()` function gives
[cut](http://www.gnu.org/manual/gawk/html_node/Cut-Program.html)
functionality to Perl.\
Usage: `split('delimeter',input,max_no_of_fields);`

#### Example

Cycle through the output of a find command and output the second dir and
put them into the array `@dirnames`:

    open(TIMELINE_PIPE,"find www/ -type f -name *.jp* -mtime 6|");
    my $i=0;my @dirnames;
    while (<TIMELINE_PIPE>) {
        chomp;
        my @dir1 = split('/',$_,3);
        my $dir2 = $name1[1];
        print "$dir2\
    ";
        push @dirnames, $dir2
    }

[Category:Perl](Category:Perl "wikilink")
