---
layout: post 
title: Apache Digest Authentication
---

Check that the auth\_user\_module and authz\_group\_module are both
loaded. If they are not listed add the following to your `httpd.conf` ,
otherwise you will see this error:
`configuration error: couldn't check access. No groups file?`

    #Added so "require valid-user" works
    LoadModule authz_user_module modules/mod_authz_user.so
    LoadModule authz_owner_module modules/mod_authz_owner.so

Create an htdigest file:

    $ htdigest -c .htdigest "Restricted" testuser
    Adding password for testuser in realm Restricted.
    New password: 
    Re-type new password: 

Example digest config which be placed within your vhost config:

    <Directory /var/www/examle.com/files>
      AuthType Digest
      AuthName "Restricted"
      #In some versions of Apache the directive AuthDigestFile is used instead of AuthUserFile got digest auth
      AuthUserFile conf/.htdigest
      Require valid-user
      AuthDigestDomain /files/ 
    </Directory>

### See Also

<http://www.linuxsecurity.com/content/view/133913/171/> [Apache,
Subversion and \"configuration error: couldn\'t check access. No groups
file?:\"](http://www.stedee.id.au/node/45)

[Category:Linux](Category:Linux "wikilink")
[Category:Web](Category:Web "wikilink")
