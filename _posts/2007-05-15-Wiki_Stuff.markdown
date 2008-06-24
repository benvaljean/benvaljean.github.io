---
layout: post 
title: Wiki Stuff
---

\_\_NOTOC\_\_

<big>**MediaWiki has been successfully installed.**</big>

Consult the [User\'s
Guide](http://meta.wikimedia.org/wiki/Help:Contents) for information on
using the wiki software.

dGsXvz dfv814t4fdfvmlfn093fvgbos

Last Update on my site. Hot Porn Video for Your, Dear Funs :) Welcome!

So, links below this is a part of my porn portal that has been updated
today 8) 1. Pictures - Hot Update. More Fresh Porn Photos - High
Quality. <http://joseffsmith.we.bs/xxx-pictures-gallerys.html> 2. Top 10
Hardcore Clips today - it\'s interesting ;)
<http://joseffsmith.we.bs/top-10-today-hardcore-porn-clips.html> 3. New!
Sexy Girls without porn content - just beautiful :)
<http://joseffsmith.we.bs/sexy-girls-non-porn-last-update-gallerys.html>
4. Certainly :) Teen Porn - today it\'s sample - Very hot 8)
<http://joseffsmith.we.bs/hot-teens-samples-video.html> 5. Just Good
Guys ;) <http://joseffsmith.we.bs/just-good-guys.html> 6. Any Porn Stuff
from any XXX Sites & Free Porn links
<http://joseffsmith.we.bs/many-porn-stuff-with-any-xxx-sites.html> Enjoy
it :)

Joseff Smith - the Best Content! Nota bene, my site updated daily,
Almost FREE! ;) . . . Most Popular Searches anal fuck anal fucking
assfucking babysitter fucking dog fuckers dogs fucking girls fuck my
wife fuck pic fuckmymom gay fuck hardcore fuck hardcore fucking hardcore
mature fucking tit fuck tit fucking women fucking dogs analfuck
analfucking assfucking babysitterfucking dogfuckers fuckpic fuckmymom
gayfuck hardcorefuck hardcorefucking titfuck titfucking beastfuckers
momsfucking assfuckingvideo dogsfuckinggirls fuckmywife
hardcorematurefucking womenfuckingdogs anal fuck sex submit.cgi anal
fucking pictures girl being anal fucked free pics of anal fucking fuck
suck sex oral anal analfuckers anal fuckin anal fuck machines anal fuck
mature milf anal fucked analfucking anal fuck analfuck analfucked fuck
birthday cards fuck an horse freefuckcams fuckers nurses fucking doctors
fist fucking girls fucking dogs moms fucking girl geting fuck pictures
fuck jokes tawnee stone fucking fuckmymom assfucking dog fuckers
granniesfucked fuckk gallery pet fucking video naruto sakura fucking
fuckingmachines.stg beast fuckers horse fucking fuckingfreemovies long
penis fucking dogfucking xxx rated fucking girls fucking horses animals
fucking babysitter fucking black trannies fucking hardfucked women
fucking animals dog fucking granny fucking footfuck machofucker horse
fuckers dogs fucking girls women fucking dogs adults fisk fucking
amateur wife fuck movies naked amateur girls fucking pictures girl being
anal fucked free pics of anal fucking fuck suck sex oral anal
analfuckers old ladys fucking big cocks free video fucking black cocks
large big cocks fucking skinny cunt fucking double dick fucking gays
fucking dicks

### Removing Main Page Title

Methods to remove the \"Main Page\" title from the main page, as
configured on Wikipedia. These examples also remove the \"siteSub\" and
\"contentSub\".

#### Using JavaScript

Add to your *LocalSettings.php*:

`$wgUseSiteJs = true;`

Edit your *MediaWiki:Common.js* system message page and insert the
javascript below.

    /* Main page hacks. Remove default "Main Page" header */
    var mpTitle = "{{MediaWiki:Mainpage}}";
    var isMainPage = (document.title.substr(0, document.title.lastIndexOf(" - ")) == mpTitle);
    var isDiff = (document.location.search && (document.location.search.indexOf("diff=") != -1 || document.location.search.indexOf("oldid=") != -1));

    if (isMainPage && !isDiff) 
    {
    document.write('<style type="text/css">/*<![CDATA[*/ #siteSub, #contentSub, h1.firstHeading { display: none !important; } /*]]>*/</style>');
    }

If this doesn\'t work, try changing {{MediaWiki:Mainpage}} to the name
of your main page. On sites set to use English, this is usually, \"Main
Page\".

#### Using CSS

In MediaWiki 1.9 and above you can remove the Main Page title using CSS.
For example, you could add the following to the *MediaWiki:Monobook.css*
system message page.

    body.page-Main_Page #siteSub, 
    body.page-Main_Page #contentSub, 
    body.page-Main_Page h1.firstHeading {
        display: none !important;
    }

Images in mediawiki:
<http://askdrwiki.com/mediawiki/index.php?title=Help:Images_and_other_Media>
