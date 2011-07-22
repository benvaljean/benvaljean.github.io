---
layout: post 
title: Check DSL Line Noise (Cisco)
---

**Line noise** occurs on ever DSL line - it is the noise or signal on
the line that is occurring when there is no transmitting upsteam nor
downstream.

    show dsl interface atmx | i Noise Margin

The **Noise Margin** is the margin in dB between the background noise
that occurs and the transmitting or receiving of data. Therefore a low
noise margin is bad and a high noise margin is good.

    cisco> show dsl interface atm0 | i Noise Margin
    Noise Margin:      9.5 dB             12.0 dB

[Category:Networking](Category:Networking "wikilink")
