---
layout: post 
title: Block dangerous/unsafe attachments (Postfix)
---

[Postfix](http://www.postfix.org/) can be configured to block
attachments with specific extensions that could be dangerous. Such as
.exe; .bat etc. The blocking is done at the MTA level, eliminating [back
scatter](Stop_Producing_Backscatter_Spam_(Exchange_2003/2007) "wikilink").

### Method

1.  Edit `/etc/postfix/main.cf` and add the following line:
        header_checks = pcre:/etc/postfix/header_checks

2.  Create a new file `/etc/postfix/header_checks` with following line:
        /^content-(type|disposition):.*name\\s*=.*\\.(exe|pif|app|asp|bat|cmd|com|cpl|csh|js|msc|prf|pst|vb|vbs|ws|wsc|wsh)/    REJECT We cannot accept executable attachments

3.  `postmap /etc/postfix/header_checks`
4.  For Debian and related distros: `apt-get install postfix-pcre` For
    other distros if the package is not available Postfix may need to be
    bulit with PRCE support: <http://www.postfix.org/PCRE_README.html> .

[Category:Linux](Category:Linux "wikilink")
[Category:Postfix](Category:Postfix "wikilink")
