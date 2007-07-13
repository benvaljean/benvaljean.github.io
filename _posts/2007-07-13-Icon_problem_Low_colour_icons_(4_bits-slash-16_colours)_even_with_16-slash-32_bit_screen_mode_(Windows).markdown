---
layout: post 
title: Icon problem: Low colour icons (4 bits/16 colours) even with 16/32 bit screen mode (Windows)
---

![16 colour icons with a 65k colour desktop behind
it](LowColourIcons.JPG "16 colour icons with a 65k colour desktop behind it"){width="200"}

### Symptoms

All icons - including your desktop, file and start menu icons - have a
low number of colours and consequently do not have the same \'quality\'
as they previously did, even in a screen mode of 16 or 32 bits (65,000+
colours.) A typicial example of this is shown to the right with 4 bit/16
colour desktop icons in front of a 16 bit/65k colour image.

### Cause

The [registry](registry "wikilink") value of \"Shell Icon BPP\" is set
incorrectly - usually to a value higher than the current screen mode.
For instance a setting of 32 on a 16 bit screen mode.

### Resolution

Increase the number of bits in the screen mode. To do this go to Control
Panel \> Display, settings tab and change the value in \'Colour
quality\' to a higher value.

**OR**

A more cleaner resoloution is to change the affected
[registry](registry "wikilink") value: HKEY\_CURRENT\_USER\\\\Control
Panel\\\\Desktop\\\\WindowMetrics\\\\\"Shell Icon BPP\" to match the
number of bits in the current screen mode. To ascertain the number of
bits in the screen mode follow the steps above.

*This specific issue refers to when all Windows icons are affected, if
you are having an issue with just some of them, it can be fixed by
[Rebuliding Icons (Windows)](rebuilding_your_icons "wikilink").*

### See Also

[Annoyances.org re: Question about \'Use True-Color
Icons\'](http://www.annoyances.org/exec/forum/win2000/1007890983)

[Category:Registry](Category:Registry "wikilink")
