---
layout: post 
title: Monitor Windows file shares (SMB) using Nagios
---

not finished

[Nagios](Nagios "wikilink") is a free open-source monitoring
system/platform.

Nagios can monitor Windows file shares (SMB) through the use of the
[check\_diskwrite2](http://exchange.nagios.org/directory/Plugins/Operating-Systems/Windows/check_diskwrite2/details)
plugin. All functonality of the file shares is monitored as the plugin
connects, creates a file, writes to a file, compares the contents to a
copy kept locally and then deletes it. If any of the tests fail an alert
is generated in Nagios.

#### Plugin installation

1.  Download from [Nagios Exchange:
    check\_diskwrite2](http://exchange.nagios.org/components/com_mtree/attachment.php?link_id=958&cf_id=24)
    or from the
    [mirror](http://ben.goodacre.name/nagios/check_diskwrite2) on this
    site and copy it to your [libexec](Nagios#Plugins "wikilink") dir.
2.  Install smbclient if not already present on your system. Type
    `whereis smbclient` to check whether it is installed.

-   Install on Debian/Ubuntu based systems: `sudo apt-get install smbfs`
-   Install on Red Hat/CentOS based systems:
    `sudo yum install samba-client`

[Category:Windows](Category:Windows "wikilink")
[Category:Nagios](Category:Nagios "wikilink")
