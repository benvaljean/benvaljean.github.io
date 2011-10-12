---
layout: post 
title: Check ADSL Line Stats (Networking)
---

#### Background

There are four properties that determine effective speed of an ADSL
line:

##### Attenuation

Line attenuation is in relation to the \"loop loss\" on your line from
the DSLAM at the Exchange all the way to your router - the lower the
figure the better. The further you are away from the exchange the higher
your attenuation figure will be as the signal loss increases.\    

It is logarithmic and each 3dB of attenuation halves the strength of the
signal power received - a line with 30dB of attenuation only receives
1/1,000th of the power.

True line attenuation is measured at the DSLAM at the exchange and this
figure should remain fairly static. Our routers can give us an
indication of how much the signal is attenuated as an average against
all the frequencies that it uses.

##### SNR / SNR Margin

Signal to Noise ratio is the measurement of the different between the
noise level and the TX (transmit) level of the signal in your line as a
ratio of each other. On a radio station the SNR is the different between
the background \'hiss\' heard between the radio station and the signal
of a radio station itself. Background noise is
electronmagnetic-radiation from a number of sources ranging from
electronic equipment to the big-bang. The SNR is best dueing the day
time when less electrical appliances are in-use.

SNR Margin is effectively the same for thing for any kind of domestic
use. SNR *margin* is the difference between the background and TC
(transnmit) values. Customer router always show this value irrigardless
of whether the term \'margin\' is seen.

##### Sync speed

This is the speed that is negotiated by your router with the line and is
dependant on the two factors above.

#### Check line stats

##### Cisco

The DSL interface is normally `atm0`, for can check this with
`sh ip int brief`. **US** refers to upsteam and **DS** refers to
downstream.

    cisco>show dsl interface atm0
    ATM0
    Alcatel 20190 chipset information
             ATU-R (DS)            ATU-C (US)
    Modem Status:     Showtime (DMTDSL_SHOWTIME)
    DSL Mode:     ITU G.992.1 (G.DMT) Annex A
    ITU STD NUM:      0x03                 0x2 
    Vendor ID:     'STMI'                 'P   '
    Vendor Specific: 0x0000                 0x0000
    Vendor Country:     0x0F                 0xB5
    Capacity Used:     83%                 82%
    Noise Margin:      9.5 dB             12.0 dB
    Output Power:     15.5 dBm             13.0 dBm
    Attenuation:     16.0 dB              6.5 dB
    Defect Status:     None                            None                        
    Last Fail Code:     None
    Watchdog Counter: 0x90
    Watchdog Resets: 0
    Selftest Result: 0x00
    Subfunction:     0x00 
    Interrupts:     7658 (0 spurious)
    PHY Access Err:     0
    Activations:     1
    LED Status:     ON
    LED On Time:     100
    LED Off Time:     100
    Init FW:     embedded
    Operation FW:     embedded
    FW Version:     2.5.42

              Interleave        Fast    Interleave        Fast
    Speed (kbps):           8128               0           832               0
    Cells:            7111309               0     308774250               0
    Reed-Solomon EC:          0               0            22               0
    CRC Errors:             18               0             3               0
    Header Errors:             14               0             1               0
    Total BER:          1367E-12         0E-0Leakage Avarage BER:      2195E-13         0E-0
    LOM Monitoring : Disabled

#### See Also

[Improve SNR](Improve_SNR_(Networking) "wikilink")

[ADSL on kitz.co.uk](http://www.kitz.co.uk/adsl/)

[Category:Networking](Category:Networking "wikilink")
