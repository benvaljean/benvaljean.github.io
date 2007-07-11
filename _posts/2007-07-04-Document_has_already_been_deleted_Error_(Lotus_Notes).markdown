---
layout: post 
title: Document has already been deleted Error (Lotus Notes)
---

When trying to delete a particular document/email within [Lotus
Notes](http://en.wikipedia.org/wiki/Lotus_Notes) the following error can
occur: **Document has already been deleted** and the document/email
cannot be deleted.

This occurs when soft deletions are enabled and orphened entries in the
view are still present; linking to documents/email when are no longer in
the database. - The emails have actually *already been* deleted, but the
entry in the view is still present. The orphaned entries are also unable
to be moved.

To fix this do one of the following, starting with the first:

1.  **Compact the database:** From within the database go to File \>
    Database \> Properties \> \"i\" tab. Click on \'% used\' , wait a
    moment and then click on compact.
2.  **Disable and then re-enable soft deletions:** From within the
    database go to File \> Database \> Properties \> Advanced /
    right-most tab. Uncheck \'Allow soft deletions\' , exit the
    database, re-open and then re-tick it.
3.  **Force a refresh of orphaned entries:** Get a user with manager
    access to the database to press Shift+Del when highlighting one of
    the documents/emails that cannot be deleted.
4.  **Force a refresh of the views:** Get a user with manager access to
    the database to press Ctrl+Shift+F9 when in the database.

### See Also

[IBM Notes Domino Forum: User cannot delete message in
inbox](http://www-10.lotus.com/ldd/nd6forum.nsf/DateAllFlatWeb/34aec46c716991988525721400477c60?OpenDocument)

[Category:Lotus Notes](Category:Lotus_Notes "wikilink")
