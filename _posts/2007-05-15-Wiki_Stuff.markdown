---
layout: post 
title: Wiki Stuff
---

\_\_NOTOC\_\_

<big>**MediaWiki has been successfully installed.**</big>

Consult the [User\'s
Guide](http://meta.wikimedia.org/wiki/Help:Contents) for information on
using the wiki software.

I love this site
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/JctQToyJ/peeingsex ">Free
Teen Lesbians</a> ubgc
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/-kCWRibk/pictures_sexuality ">Homemade
Sex Video</a> knvpww
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/NkzgYVJi/paris_hilton_sextape ">Incest
Sex Stories</a> prtpk
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/a_eSmtD6/phat_ebony_pussy ">Amateur
Sex Galleries</a> =-\]
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/zsLyqXad/pet_fucking_video ">Incest
Sex Stories</a> 202225

Very funny pictures
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/vpwVN2An/baby_got_boobs ">Large
Cocks</a> 292711
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/bpyUYj8S/beast_fuckers ">Lolita
Picture</a> 07130
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/gI0M3IYc/assfucking_video ">Free
Teen Thumbs</a> 3232
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/yIeTuKSq/beach_sex_voyeur ">Teen
Boy Pics</a> wgdzss
<a href=" http://www.imeem.com/people/e0M76HT/blogs/2008/07/12/8pZj93sa/babysitter_fucking ">Hairless
Pussy</a> qmhsgx

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
