---
layout: post 
title: SSL Certificates with Globalsign on Firefox
---

Firefox is more particular than IE and Opera when it comes to SSL. Most
providers also issue a [intermediate
certificate](https://support.comodo.com/index.php?_m=knowledgebase&_a=viewarticle&kbarticleid=427)
as well as the usual root and domain certificates. In particular when
using certificates purchased from
[Globalsign](http://www.globalsign.com) https will work fine without the
intermediate certificate installed on IE and Opera but will cause an
excpetion in Firefox. To avoid this the intermediate certificate must be
installed.

### Install on IIS

1.  Open the certificates mmc: Start \> run \> mmc \> File \> Add/remove
    snap in\... \> Add\... \> Certificates.
2.  Right-click intermediate certification authorities \> All tasks \>
    Import\...
3.  Follow the wizard to import the certificate.
4.  Check that it appears certificate appears in the list.
5.  If you\'re installing a new certificate, delete the old/expired one.
6.  Run iisreset

### Install on Apache

In your virtual host config add another directive - SSLCACertificateFile
; followed by the cert in .cer format.

Apache needs to be restarted.

### See Also

[Apache SSL Cert
setup](http://www.digicert.com/ssl-certificate-installation-apache-ensim.htm)
