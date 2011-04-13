---
layout: post 
title: Get Hard disk manufacturer and model (Linux)
---

To obtain detailed information on the hard drives installed `sdparm` or
`hdparm` can be used. Manufacturer, model, serial number and size as
well as other information is available.

#### SCSI Drives

    sdparm -a /dev/sda

#### IDE Drives

    hdparm -I /dev/hda

[Category:Linux](Category:Linux "wikilink")
