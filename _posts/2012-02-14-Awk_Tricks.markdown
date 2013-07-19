---
layout: post 
title: Awk Tricks
---

#### Delete occurances of a string

    awk '{ gsub(/string/,""); print }'

#### Replace text1 with text2

    awk '{ gsub(/text1/,text2); print }'

#### Replace text1 with text2 only lines that contain Hello

    awk '/Hello/ { gsub(/text1/,text2); print }'

#### Replace text1 with text2 only lines that do NOT contain Hello

    awk '!/Hello/ { gsub(/text1/,text2); print }'

#### Swap first field with the second field

    awk '{ temp = $1; $1 = $2; $2 = temp; print }'

#### Delete the second field

    awk '{ $2 = ""; print }'

#### Remove duplicate, nonconsecutive lines

    awk '!a[$0]++'

#### Show lines based on field-criteria

-   Show processes in uninterruptible sleep (usually IO):

<!-- -->

    ps aux|awk '{if ($8 == "D") print}'

#### Use substr with print

Useful for when combining with uniq -c for log file analysis:

    awk '{print substr($4,0,6)}' squidaccess.log | uniq -c
       2571 [14/J
       7365 [15/J
       8085 [16/J
       6537 [17/J
        200 [18/J
         90 [19/J

#### See Also

<http://www.catonmat.net/blog/awk-one-liners-explained-part-two/>

<http://www.catonmat.net/blog/awk-book/>

[Category:Linux](Category:Linux "wikilink")
