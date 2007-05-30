---
layout: post 
title: Wiki Stuff
---

\_\_NOTOC\_\_

<http://www.mediawiki.org/wiki/Manual:FAQ>
<http://www.mediawiki.org/wiki/Manual:Navigation_bar>

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
