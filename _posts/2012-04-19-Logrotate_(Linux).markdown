---
layout: post 
title: Logrotate (Linux)
---

The right way to logrotate, keep 14 days with helpful dates and the
filenames do not change every day for your logs:

    /var/log/app/app.log /var/log/app/app_something.log {
        rotate 14
        daily
        missingok
        notifempty
        sharedscripts
        postrotate
            /bin/kill -HUP `cat /var/run/app.pid 2>/dev/null` 2> /dev/null || true
        endscript
        dateext
    }

If your app has the ability to rotate logs via a command-line argument
(such as Squid) this should be used instead, or even better use
\[anacron.sourceforge.net/ Anacron\].

[Category:Linux](Category:Linux "wikilink")
