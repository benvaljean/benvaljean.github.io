---
layout: post 
title: Strip Apostrophe (or any character) in SMTP email address (Exchange 2003/2007)
---

### Background

As per RFC certain characters are not permissalbe in SMTP addresses. All
versions of Exchange automatically strip/remove invalid characters.
Apostrophes on the contrary are \'offically\' allowed however it is
general practice to not use them in smtp address as despite Exchange
handling them OK; other systems such as Watchguard will block smtp
sessions that contain an apostrophe.

### Using the %r replacement string

The replacement string in a recipient policy (Exchange 2000/2003) or an
email address policy (Exchange 2007) allow a character to be
replaced/substituted for another or simply deleted when used BEFORE the
replacement string where characters should be reaplced.

#### Syntax

\%rxy\
To replace character \"x\" with character \"y\"

\%rxx\
To strip/delete all occurances of \"x\"

-   For example to use firstname.lastname whilst stripping all
    apostrophes from the last name:

<!-- -->

    %g.%r''%s@domain.com

### Change configuration to affect all users

#### Exchange 2007

-   From
    [EMC](http://technet.microsoft.com/en-us/library/bb123762.aspx):
    Org. Config \> Hub transport \> E-mail addresses policies tab \>
    Edit
-   Select any flitering and add a very basic policy. Now rename the new
    email address policy by performing a slow double-click on it, so it
    can be renamed. Now the policy can be freely edited - something
    which the wizard does not allow to be done.

#### Exchange 2003

-   From [Server
    Manager](http://www.comptechdoc.org/os/windows/exchange/exchesm.html):
    Recipients \> Recipient Policies
-   Double click the policy to be edited, usually Default policy.
-   Add the new policy from the E-mail addresses (Policy) tab.

### See Also

-   [How to customize the SMTP e-mail address generators through
    recipient policies](http://support.microsoft.com/kb/285136/en-us)
-   [Microsoft Exchange Admin Recipient policy - Apostrophe in
    address](http://www.eggheadcafe.com/software/aspnet/30598513/recipient-policy--apostr.aspx)
-   [emails with Apostrophe in address being
    bounced](http://social.technet.microsoft.com/Forums/en-US/exchangesvradmin/thread/feeaa174-3041-4844-86f2-7c343fccf2b4)
-   [Beware of the
    apostrophe](http://searchexchange.techtarget.com/tip/0,289483,sid43_gci1009952,00.html)

[Category:Exchange](Category:Exchange "wikilink")
