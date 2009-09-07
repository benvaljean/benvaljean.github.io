---
layout: post 
title: Rewrite on IIS that actually works
---

It is amazing to think that before IIS7 (Server 2008 / Vista) there was no native rewrite URL support for IIS.

==mod_rewrite for IIS==
There are many tools available to give rewrite functionality for IIS, most of which I have tried and do not work properly or do not fully support [http://www.regular-expressions.info/ regex]. The best tool I have found for the job is [http://www.codeplex.com/IIRF IIRF]. Like other tools available of this type it loads through an ISAPI filter extension - but unlike others '''it actually works'''. There are a few nuances to be aware of though.

==Installation==
#Download and extract to any location eg. C:\\Rewrite: http://iirf.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=29936#DownloadId=74545
#Load IIS console: Start > Run > %SystemRoot%\\system32\\inetsrv\\iis.msc
#Right-click 'Web sites' > ISAPI Filters > Add
#Type a name to recognise it by under 'Filter name' and select the IsapiRewrite4.dll file inside the lib folder of the extracted archive under 'Executable'. The filter may not appear to have loaded OK straight away, this is OK.
#Go to 'Web service extensions' in the main window.
#Click 'Add a new Web Service extension...'
#Type in the same details as before, ensure the allow checkbox is ticked.
#The config file is not created for you, the rewriter looks for a file called IsapiRewrite4.ini in the same folder as the IsapiRewrite4.dll file itself.

==Notes==
*The rewriter watches for changes in the ini file - no need to restart IIS.
*The rewrite log filename must be set to iirfLog.out and NOT in a root folder else it will not log anything.
*Use the TestParse.exe programme inside the bin directory to test your configuration first. The file must be in the same dir as IsapiRewrite4.dll .
*It is not 100% copy of mod_rewrite - such a thing does not exist. This is the nearest I have found. For instance <tt>RewriteCond %{SERVER_PORT} !^443$ </tt>will not hit the appropriate rule if the port is 80, which of course it should do. I worked around this by using <tt>RewriteCond %{SERVER_PORT} ^80$ </tt>instead as our server only needs to listen on port 80.

==Example working configuration of IIRF on IIS on Windows==
<pre>
#Enable rewrite logging, very useful. 5 is very verbose, set to 3 unless troubleshooting.
RewriteLog  c:\    emp\\iirfLog.out
RewriteLogLevel 5

#testing
#redirects /misc/anything to /misctest/anything
#will not redirect /misc to /misctest due to the tailing slash
RewriteRule ^/misc/(.*)$ /misctest/$1 [I]

#Rewrite all traffic to SSL
RewriteCond %{SERVER_PORT} ^80$
RedirectRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301]
</pre>
==Rewrite the base-URL (only) for a specific hostname==
In Apache the first line would not be required if a vhost configuration is being used. In IIRF the rewrites cannot be encapsulated within vhosts as this configuration does not exist of course. This will rewrite the base-url (only) to http://www.example.com/test when the hostname is 'www.testing.com':
<pre>
RewriteCond %{HTTP_HOST} ^www\\.testing\\.com$
RedirectRule ^/$ http://www.example.com/test [R]</pre>
==Rewrite all URLs for a domain to a holding page==
A situation can arise where all URLs on a domain need to be diverted/rewritten to the same URL, such as a holding page.
<pre>
RewriteCond %{HTTP_HOST} ^test\\.jgpskills\\.co\\.uk$
RedirectRule ^/(.*)$ /
</pre>
This does not cause a rewrite loop as the pattern-match is for a "/" and one or more characters but not for only the "/".
==Rewrite all domains to SSL, excluding one domain==
<pre>
RewriteCond %{SERVER_PORT} ^80$
RewriteCond %{HTTP_HOST} ^(?!nosslsite\\.company\\.co\\.uk)(.+)$
RedirectRule ^/(.*)$ https://%{HTTP_HOST}/$1 [R=301]

==See Also==
[[Apache Rewrite]]
[[Category:Windows]][[Category:Web]]
