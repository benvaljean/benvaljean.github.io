---
layout: post 
title: Linux System Troubeshooting:Example strace output
---

          1 exampleusername@ghost:/usr/local/nagios/libexec$ strace -e open tsql -S testconfig -U test -P test
          2 open("/etc/ld.so.cache", O_RDONLY)      = 3
          3 open("/lib/tls/i686/cmov/librt.so.1", O_RDONLY) = 3
          4 open("/lib/tls/i686/cmov/libpthread.so.0", O_RDONLY) = 3
          5 open("/lib/tls/i686/cmov/libc.so.6", O_RDONLY) = 3
          6 open("/usr/local/etc/locales.conf", O_RDONLY|O_LARGEFILE) = 3
          7 open("/usr/lib/locale/locale-archive", O_RDONLY|O_LARGEFILE) = -1 ENOENT (No such file or directory)
          8 open("/usr/share/locale/locale.alias", O_RDONLY) = 3
          9 open("/usr/lib/locale/en_GB.UTF-8/LC_IDENTIFICATION", O_RDONLY) = -1 ENOENT (No such file or directory)
         10 open("/usr/lib/locale/en_GB.utf8/LC_IDENTIFICATION", O_RDONLY) = 3
         11 open("/usr/lib/gconv/gconv-modules.cache", O_RDONLY) = 3
         12 open("/usr/lib/locale/en_GB.UTF-8/LC_MEASUREMENT", O_RDONLY) = -1 ENOENT (No such file or directory)
         13 open("/usr/lib/locale/en_GB.utf8/LC_MEASUREMENT", O_RDONLY) = 3
         14 open("/usr/lib/locale/en_GB.UTF-8/LC_TELEPHONE", O_RDONLY) = -1 ENOENT (No such file or directory)
         15 open("/usr/lib/locale/en_GB.utf8/LC_TELEPHONE", O_RDONLY) = 3
         16 open("/usr/lib/locale/en_GB.UTF-8/LC_ADDRESS", O_RDONLY) = -1 ENOENT (No such file or directory)
         17 open("/usr/lib/locale/en_GB.utf8/LC_ADDRESS", O_RDONLY) = 3
         18 open("/usr/lib/locale/en_GB.UTF-8/LC_NAME", O_RDONLY) = -1 ENOENT (No such file or directory)
         19 open("/usr/lib/locale/en_GB.utf8/LC_NAME", O_RDONLY) = 3
         20 open("/usr/lib/locale/en_GB.UTF-8/LC_PAPER", O_RDONLY) = -1 ENOENT (No such file or directory)
         21 open("/usr/lib/locale/en_GB.utf8/LC_PAPER", O_RDONLY) = 3
         22 open("/usr/lib/locale/en_GB.UTF-8/LC_MESSAGES", O_RDONLY) = -1 ENOENT (No such file or directory)
         23 open("/usr/lib/locale/en_GB.utf8/LC_MESSAGES", O_RDONLY) = 3
         24 open("/usr/lib/locale/en_GB.utf8/LC_MESSAGES/SYS_LC_MESSAGES", O_RDONLY) = 3
         25 open("/usr/lib/locale/en_GB.UTF-8/LC_MONETARY", O_RDONLY) = -1 ENOENT (No such file or directory)
         26 open("/usr/lib/locale/en_GB.utf8/LC_MONETARY", O_RDONLY) = 3
         27 open("/usr/lib/locale/en_GB.UTF-8/LC_COLLATE", O_RDONLY) = -1 ENOENT (No such file or directory)
         28 open("/usr/lib/locale/en_GB.utf8/LC_COLLATE", O_RDONLY) = 3
         29 open("/usr/lib/locale/en_GB.UTF-8/LC_TIME", O_RDONLY) = -1 ENOENT (No such file or directory)
         30 open("/usr/lib/locale/en_GB.utf8/LC_TIME", O_RDONLY) = 3
         31 open("/usr/lib/locale/en_GB.UTF-8/LC_NUMERIC", O_RDONLY) = -1 ENOENT (No such file or directory)
         32 open("/usr/lib/locale/en_GB.utf8/LC_NUMERIC", O_RDONLY) = 3
         33 open("/usr/lib/locale/en_GB.UTF-8/LC_CTYPE", O_RDONLY) = -1 ENOENT (No such file or directory)
         34 open("/usr/lib/locale/en_GB.utf8/LC_CTYPE", O_RDONLY) = 3
         35 locale is "en_GB.UTF-8"
         36 locale charset is "UTF-8"
         37 open("/etc/nsswitch.conf", O_RDONLY)    = 3
         38 open("/etc/ld.so.cache", O_RDONLY)      = 3
         39 open("/lib/tls/i686/cmov/libnss_compat.so.2", O_RDONLY) = 3
         40 open("/lib/tls/i686/cmov/libnsl.so.1", O_RDONLY) = 3
         41 open("/etc/ld.so.cache", O_RDONLY)      = 3
         42 open("/lib/tls/i686/cmov/libnss_nis.so.2", O_RDONLY) = 3
         43 open("/lib/tls/i686/cmov/libnss_files.so.2", O_RDONLY) = 3
         44 open("/etc/passwd", O_RDONLY|0x80000 /* O_??? */) = 3
    *    45 open("/home/exampleusername/.freetds.conf", O_RDONLY|O_LARGEFILE) = -1 ENOENT (No such file or directory)
    *    46 open("/usr/local/etc/freetds.conf", O_RDONLY|O_LARGEFILE) = 3
         47 open("/etc/passwd", O_RDONLY|0x80000 /* O_??? */) = 3
         48 open("/home/exampleusername/.interfaces", O_RDONLY|O_LARGEFILE) = -1 ENOENT (No such file or directory)
         49 open("/etc/freetds/interfaces", O_RDONLY|O_LARGEFILE) = -1 ENOENT (No such file or directory)
         50 open("/etc/resolv.conf", O_RDONLY)      = 3
         51 open("/etc/host.conf", O_RDONLY)        = 3
         52 open("/etc/hosts", O_RDONLY|0x80000 /* O_??? */) = 3
         53 open("/etc/ld.so.cache", O_RDONLY)      = 3
         54 open("/lib/tls/i686/cmov/libnss_dns.so.2", O_RDONLY) = 3
         55 open("/lib/tls/i686/cmov/libresolv.so.2", O_RDONLY) = 3
         56 open("/etc/resolv.conf", O_RDONLY)      = 3
         57 open("/usr/lib/gconv/ISO8859-1.so", O_RDONLY) = 3
         58 There was a problem connecting to the server
         59 Process 30147 detached
