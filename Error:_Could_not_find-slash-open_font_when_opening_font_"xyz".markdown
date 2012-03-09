---
layout: post 
title: Error: Could not find/open font when opening font "xyz"
---

f1\@goodacre.name,===Symptom=== When trying to plot with gnuplot the
following error can appear:

        Could not find/open font when opening font "xyz", using
        internal non-scalable font

#### Cause

gnuplot cannot find the font, either due to referencing a font that is
not free and therefore does not exist on Linux (such as arial) or your
environment variables are not set correctly.

#### Resolution

Look for your fonts dir, this is is usually `/usr/share/fonts` If it is
empty you will need to download a free TTF font.

-   Check the environment variables `$GDFONTPATH` and
    `$GNUPLOT_DEFAULT_GDFONT`

<!-- -->

    $ ls /usr/share/fonts/truetype
    arielfree.ttf
    $ GDFONTPATH='/usr/share/fonts/truetype'
    $ GNUPLOT_DEFAULT_GDFONT=arielfree

#### References

<http://gnuplot.sourceforge.net/faq/faq.html#SECTION00091000000000000000>

[Category:Linux](Category:Linux "wikilink")
