---
layout: post 
title: Wiki Stuff
---

\_\_NOTOC\_\_

<big>**MediaWiki has been successfully installed.**</big>

Consult the [User\'s
Guide](http://meta.wikimedia.org/wiki/Help:Contents) for information on
using the wiki software.

### Getting started

-   [Configuration settings
    list](http://www.mediawiki.org/wiki/Help:Configuration_settings)
-   [MediaWiki FAQ](http://www.mediawiki.org/wiki/Help:FAQ)
-   [MediaWiki release mailing
    list](http://mail.wikimedia.org/mailman/listinfo/mediawiki-announce)

<!-- -->

-   <http://www.mediawiki.org/wiki/Manual:FAQ>
-   <http://www.mediawiki.org/wiki/Manual:Navigation_bar>
-   <http://meta.wikimedia.org/wiki/MediaWiki_FAQ>

Edit <http://www.mediawiki.org/wiki/MediaWiki:Sidebar>

#### How do I put a text message (sitenotice) on every page?

Put a text in the MediaWiki:Sitenotice page. It will be displayed on top
of every article page.

#### How do I change the main page?

By default, MediaWiki looks for a page with the title Main Page and
serves this as the default page. This can be changed by altering the
contents of MediaWiki:Mainpage to point to a different title. This will
not affect any of the links of the main navigation bar, including the
\'Main Page\' link included there at install time; to change these
links, edit MediaWiki:Sidebar.

<http://www.mediawiki.org/wiki/MediaWiki:Common.css>

#### How do I add/remove tabs in general?

To (for example) remove the talk tab and then add one that always goes
to the main page you would save this code in (for example)
extensions/AR-Tabs.php:

`$wgHooks['SkinTemplateContentActions'][] = 'ReplaceTabs';`\
`function ReplaceTabs ($content_actions) {  `\
` unset( $content_actions['talk'] );    //only this to remove an action`\
`    $maintitle = Title::newFromText(wfMsg('mainpage') );`\
`     $main_action['main'] = array(`\
`       'class' => false or 'selected',    //if the tab should be highlighted`\
`       'text' => wfMsg('sitetitle'),     //what the tab says`\
`       'href' => $maintitle->getFullURL(),   //where it links to`\
`     );`\
`     $content_actions = array_merge( $main_action, $content_actions);   //add a new action`\
`}`

and then add

`require_once("extensions/AR-Tabs.php");`

to the bottom of LocalSettings.php

#### How do I remove the \"Talk for this IP\" link at the top right when \$wgDisableAnonTalk is true

In SkinTemplate.php line 489 (in version 1.9.2 and 1.9.3) change

       global $wgTitle, $wgShowIPinHeader;

to

       global $wgTitle, $wgShowIPinHeader, $wgDisableAnonTalk;

and lines 547 - 554 from

         $usertalkUrlDetails = $this->makeTalkUrlDetails($this->userpage);
         $href = &$usertalkUrlDetails['href'];
         $personal_urls['anontalk'] = array(
           'text' => wfMsg('anontalk'),
           'href' => $href,
           'class' => $usertalkUrlDetails['exists']?false:'new',
           'active' => ( $pageurl == $href )
         );

to (adding the if statement and indenting existing lines)

         if( !$wgDisableAnonTalk ) {
           $usertalkUrlDetails = $this->makeTalkUrlDetails($this->userpage);
           $href = &$usertalkUrlDetails['href'];
           $personal_urls['anontalk'] = array(
            'text' => wfMsg('anontalk'),
            'href' => $href,
            'class' => $usertalkUrlDetails['exists']?false:'new',
            'active' => ( $pageurl == $href )
           );
         };

The logo image should be 135 pixels square.

[Word2Wiki macro](http://meta.wikimedia.org/wiki/Word_macros#Word2Wiki)

### HTTPS on Login only

For having encryption on password sending this could be useful (add to
LocalSettings.php)

    # take care of https login and back to http after 
    # (Yedidia Klein)
    $ServerName=$_SERVER['HTTP_HOST'];
    if ((substr($_GET['title'],-10,10) == ":Userlogin") && ($_SERVER['HTTPS'] != "on"))
            header("Location: https://$ServerName".$_SERVER['REQUEST_URI']);
    else if ((substr($_GET['title'],-10,10) != ":Userlogin") && ($_SERVER['HTTPS'] == "on"))
            header("Location: http://$ServerName".$_SERVER['REQUEST_URI']);

:   This is a nice start but too simplistic. It will fail if you\'re
    using
    [Using\_a\_very\_short\_URL](Using_a_very_short_URL "wikilink") or
    [Eliminating\_index.php\_from\_the\_url](Eliminating_index.php_from_the_url "wikilink")
    because the page title is no longer in query string. It will also
    serve CSS stylesheets and JavaScript files insecurely (via HTTP) on
    the HTTPS page, making Firefox warn you that the page is only
    \"partially encrypted\" (a padlock icon with a slash through it).
    You will also get PHP warnings that the \'title\' array element
    doesn\'t exist, if you hit a wiki page with no \'title\' query
    parameter.

<!-- -->

:   The following is an \"extension\" that handles both these problems.
    Call it whatever you want and include it in LocalSettings.php.
    [Maiden taiwan](User:Maiden_taiwan "wikilink") 18:11, 6 March 2007
    (UTC)

<!-- -->

:   

    :   Update - the extension kills the \"Remember my login\" checkbox
        feature \-- you lose your sessions because cookies are created
        as secure on the https page, so the http pages can\'t access
        them. I\'ve updated the code below. [Maiden
        taiwan](User:Maiden_taiwan "wikilink") 04:45, 16 March 2007
        (UTC)

<!-- -->

    <?php
    # Secure the login page.

    # Secure cookies hurt us because they are set on the https page
    # but inaccessible from the http page, so we lose our previous session.
    $wgCookieSecure = false;

    # Don't process JavaScript and CSS files.
    # Otherwise, a secure page will be tagged as "partially secure" because these
    # files are being hit via http.
    if (checkQS('gen', 'js')) {return;}
    if (checkQS('gen', 'css') || checkQS('ctype', 'text/css')) {return;}

    # Get page title from query string.
    $pageTitle = array_key_exists('title', $_GET)
         ? $_GET['title']
         : "";

    # Get server variables
    $domain = $_SERVER['HTTP_HOST'];
    $uri = $_SERVER['REQUEST_URI'];

    # Are we on the sign-in page or not?
    # Logic works for everything except Special pages which apparently don't
    # even run LocalSettings.php.
    $onSignInPage = false;
    $signInPageName = 'special:userlogin';  // lowercase on purpose
    if ( strtolower($pageTitle) == $signInPageName ) {
      $onSignInPage = true;
    } elseif ( strstr(strtolower($uri), "/$signInPageName") ) {
      $onSignInPage = true;
    } else {
      $onSignInPage = false;
    }

    # Secure only the Special:Userlogin page.
    # Un-secure all other pages.
    if ( !checkServerVariable('HTTPS', 'on') && $onSignInPage ) {
      header('Location: https://' . $domain . $uri);
    } elseif ( checkServerVariable('HTTPS', 'on') && ! $onSignInPage ) {
      header('Location: http://' . $domain . $uri);
    } else {
      // nothing
    }

    function checkQS($key, $value) {
      return checkArrayValue($_GET, $key, $value);
    }

    function checkServerVariable($var, $value) {
      return checkArrayValue($_SERVER, $var, $value);
    }

    function checkArrayValue($arr, $key, $value) {
      return array_key_exists($key, $arr) && $arr[$key] == $value;
    }

    ?>

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
