---
layout: post 
title: Associative Arrays (Perl)
---

    my %splitfilenames (1, "allpics.aa",
                2, "allpics.ab",
                3, "allpics.ac",
                4, "allpics.ad",
                5, "allpics.ae");

To add a single value at a time (useful in loops):

    my %splitfilenames;
    $splitfilenames{1) = "allpics.aa";

`$splitfilenames{2}` would then return \"allpics.ab\"

[Category:Perl](Category:Perl "wikilink")
