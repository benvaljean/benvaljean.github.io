---
layout: post 
title: Your availability time range is invalid
---

f1\@goodacre.name,![Availability
issue](Availissue_LotusNotes.JPG "fig:Availability issue") From within
Preferences in a database in [Lotus
Notes](http://en.wikipedia.org/wiki/Lotus_Notes) the following error /
dialog can appear: **Your availability time range is invalid, please
correct.**

This dialog appears from within anywhere within Preferences - even if
you are not editing availability information. This is due to Notes
checking the validation for \'every field\' after editing any field.

The error occurs when invalid time periods have been entered within
Tools \> Preferences \> Calendar & To Do \> Scheduling; see screenshot.
Invalid periods usually involve a mixture of 24-hour and 12-hour times:

Valid:\
09:00 - 12:00, 13:00 - 17:30\
09:00 - 12:00, 13:00 - 5PM\
Invalid:\
09:00 - 12:00, 13:00 - 05:00\
09:00 - 12:00, 13:00 - 0:00

For an unknown reason Notes also checks the validation of fields where
the checkbox has not been ticked, ensure these are checked too.

[Category:Lotus Notes](Category:Lotus_Notes "wikilink")
