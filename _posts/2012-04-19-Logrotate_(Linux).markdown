---
layout: post 
title: Logrotate (Linux)
---

Keep 14 days with helpful dates and the filenames do not change every
day for your logs:

    /var/log/app/app.log /var/log/app/app_something.log {
        rotate 14
        daily
        dateext
        compress
        missingok
        notifempty
        sharedscripts
        postrotate
            PIDFILE='/var/run/app/app.pid'
            [ -f ${PIDFLIE} ] && /bin/kill -USR1 $(cat ${PIDFILE})
        endscript
        dateext
    }

If the app has the ability to rotate logs via a command-line argument
(such as Squid) this could be used instead, or even better use
[Cronolog](http://cronolog.org).

#### Test config

    /usr/sbin/logrotate -d /etc/logrotate.conf

[Category:Linux](Category:Linux "wikilink")
