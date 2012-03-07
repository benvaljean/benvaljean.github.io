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

#### See Also

<http://www.catonmat.net/blog/awk-one-liners-explained-part-two/>

<http://www.catonmat.net/blog/awk-book/>

[Category:Linux](Category:Linux "wikilink")
