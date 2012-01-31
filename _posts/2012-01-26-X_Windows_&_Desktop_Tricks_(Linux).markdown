---
layout: post 
title: X Windows & Desktop Tricks (Linux)
---

#### Restart X without restarting machine

To get a console press Ctrl + Alt + F1, depending on your desktop
environment:

-   LightDM - Ubuntu 11.10+ `sudo /etc/init.d/lightdm restart`
-   Gnome: `sudo /etc/init.d/gdm restart`
-   KDE: `sudo /etc/init.d/kdm restart`

#### Install custom GNOME screensaver

GNOME screensavers have *screensaver engines* which are executable which
are run to display the screensaver graphics.

-   Ascertain screensaver engines directory

<!-- -->

    pkg-config --variable=privlibexecdir gnome-screensaver

Each screensaver has a `xyz.desktop` file with options such as and
parameters that should be used

-   Ascertain screensaver themes directory

<!-- -->

    pkg-config --variable=themesdir gnome-screensaver

##### See Also

<http://library.gnome.org/admin/system-admin-guide/stable/screensavers-3.html.en>

[Category:Linux](Category:Linux "wikilink")
