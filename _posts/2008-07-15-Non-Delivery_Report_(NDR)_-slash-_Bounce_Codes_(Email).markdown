---
layout: post 
title: Non-Delivery Report (NDR) / Bounce Codes (Email)
---

{| {{table}}
| align="center" style="background:#f0f0f0;"|'''First digit:'''
|-
| 
|-
| 2.x.x                              successful transfer 
|-
| 4.x.x                              persistent failure 
|-
| 5.x.x                              permanent failure
|-
| 
|-
| align="center" style="background:#f0f0f0;"|'''Second and Third digits:'''
|-
| x.1.0                              other address status
|-
| x.1.1                              bad destination mailbox address
|-
| x.1.2                              bad destination system address
|-
| x.1.3                              bad destination mailbox address syntax
|-
| x.1.4                              destination mailbox address ambiguous
|-
| x.1.5                              destination mailbox address valid
|-
| x.1.6                              mailbox has moved
|-
| x.1.7                              bad sender’s address syntax
|-
| x.1.8                              bad sender’s system address
|-
| x.2.0                              other or undefined mailbox status
|-
| x.2.1                              mailbox disabled, not accepting messages. See: [[Bounce 5.2.1 when emailing a public folder (Exchange)]]
|-
| x.2.2                              mailbox full
|-
| x.2.3                              message length exceeds administrative limit
|-
| x.2.4                              mailing list expansion problem
|-
| x.3.0                              other or undefined mail system status
|-
| x.3.1                              mail system full
|-
| x.3.2                              system not accepting network messages
|-
| x.3.3                              system not capable of selected features
|-
| x.3.4                              message too big for system
|-
| x.4.0                              other or undefined network or routing status
|-
| x.4.1                              no answer from host
|-
| x.4.2                              bad connection
|-
| x.4.3                              routing server failure
|-
| x.4.4                              unable to route
|-
| x.4.5                              network congestion
|-
| x.4.6                              routing loop detected
|-
| x.4.7                              delivery time expired
|-
| x.5.0                              other or undefined protocol status
|-
| x.5.1                              invalid command
|-
| x.5.2                              syntax error
|-
| x.5.3                              too many recipients
|-
| x.5.4                              invalid command arguments
|-
| x.5.5                              wrong protocol version
|-
| x.6.0                              other or undefined media error
|-
| x.6.1                              media not supported
|-
| x.6.2                              conversion required and prohibited
|-
| x.6.3                              conversion required but not supported
|-
| x.6.4                              conversion with loss performed
|-
| x.6.5                              conversion failed
|-
| x.7.0                              other or undefined protocol status
|-
| x.7.1                              delivery not authorized, message refused
|-
| x.7.2                              mailing list expansion prohibited
|-
| x.7.3                              security conversion required but not possible
|-
| x.7.4                              security feature not supported
|-
| x.7.5                              cryptographic failure
|-
| x.7.6                              cryptographic algorithm not supported
|-
| x.7.7                              message integrity failure
|}

[[Category:Exchange]]
