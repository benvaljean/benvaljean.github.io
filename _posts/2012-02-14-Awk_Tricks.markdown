---
layout: post 
title: Awk Tricks
---

#### Delete occurances of a string

    awk '{ gsub(/string/,""); print }'

#### Replace text1 with text2

    awk '{ gsub(/string/,text2); print }'

#### Replace text1 with text2 only lines that contain Hello

    awk '/Hello/ { gsub(/string/,text2); print }'

#### Replace text1 with text2 only lines that do NOT contain Hello

    awk '!/Hello/ { gsub(/string/,text2); print }'

#### Swap first field with the second field

    awk '{ temp = $1; $1 = $2; $2 = temp; print }'

#### Delete the second field

    awk '{ $2 = ""; print }'

#### Remove duplicate, nonconsecutive lines

    awk '!a[$0]++'

[Category:Linux](Category:Linux "wikilink")
