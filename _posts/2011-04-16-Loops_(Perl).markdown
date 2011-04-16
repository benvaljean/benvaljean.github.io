---
layout: post 
title: Loops (Perl)
---

#### For loops (indices)

Indices should be avoided in Perl, as better alternatives exist

    my $pagecount = 20;
    my @onetopagecount = (1 .. $pagecount);
    for my $i (@onetopagecount) { &printpage($i,$pagecount); }

#### Foreach loops

    my $pagecount = 20;
    my @onetopagecount = (1 .. $pagecount);
    foreach $page (@onetopagecount) { &printpage($page,$pagecount); }

#### While loops

While there is standard input, read into \$line variable [^1]

            while $line ( <STDIN> )  
            {                            
               chomp $line;
               print $line;             
            } 

[Category:Perl](Category:Perl "wikilink")

[^1]: <http://pages.cs.wisc.edu/~hasti/cs368/Perl/notes/lec02.html>
