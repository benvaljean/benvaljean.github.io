---
layout: post 
title: PDF Printing (Vista)
---

From
<http://forums.microsoft.com/TechNet/ShowPost.aspx?PostID=1926610&SiteID=17>

Print spooler keeps stopping after every event ( open printer window,
click on properties, print test page, etc.) I can restart the print
spooler service, after each event but at this rate it takes four or five
steps to print a document. I\'ve tried uninstalling and reinstalling the
printer/drivers (which of course invovles repeated starting of the
spooler service), I\'ve downloaded the lastest drivers from HP, and have
even tried reinstalling my operating system. Vista, business edition.
Nothing worked for longer than two print cycles! Please help.

\--Lincoln

`    Report Abuse    `\
\
\
\
` 02 Aug 2007, 5:24 PM UTC  `

DanITSec

Posts 1 Re: Vista \-- print spooler service constantly stops. I cannot
print.

` Was this post helpful ?      `\
\
\
`I continue to have the same problem (Vista Ultimate) but only when trying to print from a browser window.  I have taken the folling actions to try to determine the source of the problem:  I have disabled all add-ins and re-enabled them one by one.  None of the add-ins seem to be the culprit.  I have a Canon 6150 Ink Jet and a Samsung Network Laser printer and an app know as print to PDF.  All drivers are current.  My work around (until MS fixes the problem) is to copy the contents of the web page to Word and print from there.  I restart the spooler from the services screen.  My guess is that somehow the print spooler has become corrupt.  The silence from Microsoft if deafining.`

------------------------------------------------------------------------

D. Orr

`    Report Abuse    `\
\
\
\
` 21 Aug 2007, 5:15 PM UTC  `

Pieranr

Posts 1

`Re: Vista -- print spooler service constantly stops. I cannot print. `\
` Was this post helpful ?      `\
\
\
`I had a similar problem using a Toshiba studio 451c network pritner.  Even with the latest driver I could not get it to stop crashing the spooler until I tired this:`

In windows features make sure LPD print services and LPR port monitor
are checked

In printers, right click on printer, runa as adminstrator, properties,
advanced

Uncheck spool print docs

Check print directly to printer.

While not ideal for printing effectively, it did stop teh spooler
probelm. After 4 hours with tech services they recommended a reload of
Vista! Found this one myself.

`    Report Abuse    `\
\
\
\
` 24 Aug 2007, 10:41 PM UTC  `

MikeDelewey

Posts 1 Re: Vista \-- print spooler service constantly stops. I cannot
print.

` Was this post helpful ?      `\
\
\
`I has this problem as well.  Thought it could be a virus but it wasn't.  It turned out to be a driver Windows was loading on startup.  `

How I solved it:

Start - Run - msconfig

In General Tab select \'Selective startup\' and uncheck \'Load startup
items\"

Click on \'Services\' tab

Check box \'Hide all Microsoft services\'

You will now have a list of non MS drivers.

This is a problem of elimination.

Uncheck a number of items

Click on OK

System will ask to restart.

Restart

Keep doing this until you have found the offending driver(s), and are
able to print

Once you found it leave it unchecked.

Go back to the \'General\' tab and check \'Normal start up.

Search for the file and rename it.

Try and identify what driver this was, buy doing a search. You should
rename it. It could be a driver that is incompatable with Vista, and
needs replacing. The Vista compatabiity test is not accurate.

Hope this solves your problem

------------------------------------------------------------------------

Mike

`    Report Abuse    `\
\
\
\
` 25 Aug 2007, 7:29 PM UTC  `

sam4u2

Posts 1

`Re: Vista -- print spooler service constantly stops. I cannot print. `\
` Was this post helpful ?      `\
\
\
`THANK YOU`

`    Report Abuse    `\
\
\
\
` 17 Oct 2007, 11:05 PM UTC  `

Charlie Meredith

Posts 1 Re: Vista \-- print spooler service constantly stops. I cannot
print.

` Was this post helpful ?      `\
\
\
`Did you ever get a fix for this problem, as I now have the same problem?`

------------------------------------------------------------------------

Dumb MS Vista User

`    Report Abuse    `\
\
\
\
` 13 Nov 2007, 5:55 PM UTC  `

Home\_Systems\_Inc

Posts 2

`Re: Vista -- print spooler service constantly stops. I cannot print. `\
` Was this post helpful ?      `\
\
\
`We received a HOTFIX from Microsoft that did not work!!!`

We can start the print spooler but it just stops seconds later.

I erased all my printers in Vista and when I try to install any printer
I still get the error. We can\'t install any prints at all!

run=services.msc to start printer splooler

nahotfx\@microsoft.com wrote:

Hello,

The hot fix for your issue has been packaged and placed on an HTTP site
for you to download.

WARNING: This fix is not publicly available through the Microsoft
website as it has not gone through full Microsoft regression testing. If
you would like confirmation that this fix is designed to address your
specific problem, or if you would like to confirm whether there are any
special compatibility or installation issues associated with this fix,
you are encouraged to speak to a Support Professional in Product Support
Services.

The package is password protected so be sure to enter the appropriate
password for each package. To ensure the right password is provided cut
and paste the password from this mail.

NOTE: Passwords expire every 7 days so download the package within that
period to insure you can extract the files. If you receive two passwords
it means you are receiving the fix during a password change cycle. Use
the second password if you download after the indicated password change
date.

Package:

------------------------------------------------------------------------

KB Article Number(s): 933454 Language: All (Global) Platform: i386

NOTE: Be sure to include all text between \'(\' and \')\' when
navigating to this hot fix location!

Thanks!

`    Report Abuse    `\
\
\
\
` 14 Nov 2007, 1:53 PM UTC  `

XBlueGuy

Posts 1 Re: Vista \-- print spooler service constantly stops. I cannot
print.

` Was this post helpful ?      `\
\
\
`I am not very technically savy when it comes to the inner workings of computers.  I am also having this problem, and very frustrated.  I am now not able to print AT ALL.  What is Microsoft's deal?  Have they figured out a resolution to this yet?`

`    Report Abuse    `\
\
\
\
` 28 Dec 2007, 4:38 PM UTC  `

Sea\_Angel101

Posts 1

`Re: Vista -- print spooler service constantly stops. I cannot print. `\
` Was this post helpful ?      `\
\
\
`Yeah i just upgraded my computer to windows vista, yay, anyways i have the smae problem. everytime i try to install my printer i keep getting a message saying my printer spool isnt functioning or somthing like that and no matter what i do it wont work...i have no clue on what to do except buy a new printer, but that would cost a lot of money`

`    Report Abuse    `\
\
\
\
` 07 Jan 2008, 10:30 PM UTC  `

JeffBair66762

Posts 1 Re: Vista \-- print spooler service constantly stops. I cannot
print.

` Was this post helpful ?      `\
\
\
` `

It appears that the printer driver for the Toshiba 452 I had was
corrupted or still only compatible with Windows XP. I tried to delete
the printer and had the spooler die every time I tried to delete it . To
get around this issue I had to change the driver on that printer then
delete it. this worked fine for me after that. Then I deleted the print
driver and the package. Toshiba was late in getting suitable print
drivers out for Vista, much like HP. Everything seems fin after I
deleted the in compatable print drivers.
