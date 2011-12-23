---
layout: post 
title: Count Network connections by state (Linux)
---

To display a count of all network connections by their state:

    $ sudo netstat -ant | awk '{print $6}' | sort | uniq -c | sort -n
          1 established)
          1 Foreign
          2 SYN_SENT
          6 LISTEN
         62 CLOSING
        185 CLOSE_WAIT
        311 FIN_WAIT2
        498 SYN_RECV
        515 LAST_ACK
       1882 TIME_WAIT
       2869 FIN_WAIT1
       5622 ESTABLISHED

Onbviously the top two entries can be ignored. This is very useful for
diagnosing tcp stack issues.

[Category:Linux](Category:Linux "wikilink")
