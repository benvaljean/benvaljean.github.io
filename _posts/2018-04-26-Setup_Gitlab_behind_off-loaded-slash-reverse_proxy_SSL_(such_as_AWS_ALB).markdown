---
layout: post 
title: Setup Gitlab behind off-loaded/reverse proxy SSL (such as AWS ALB)
---

Setup [Gitlab](http://gitlab.com) behind off-loaded SSL or a
reverse-proxy/load-balancer where the SSL is being terminated, such as
when being used behind an AWS ALB that is performing SSL:

In this example nginx is setup to redirect http to https and forward
specific headers that the ALB adds to the http request. The real\_ip
directives configure gitlab to watch for this header when the request is
from the addresses in `real_ip_trusted_addresses` for designating the
real ip. `listen_https` to false informs nginx to not setup ssl
certificates using let\'s encrypt.

`/etc/gitlab/gitlab.rb`

    external_url 'https://git.company.com'

    nginx['redirect_http_to_https'] = true
    nginx['proxy_set_headers'] = {
      "X-Forwarded-Proto" => "http",
      "X-Forwarded-Port" => "80"
     }

    #Add ALB

    nginx['real_ip_trusted_addresses'] = [ '192.168.0.0/27' ]
    nginx['real_ip_header'] = 'X-Forwarded-For'
    nginx['real_ip_recursive'] = 'on'

    nginx['listen_port'] = 80
    nginx['listen_https'] = false

Apply the changes with `sudo gitlab-ctl reconfigure`

[Category:Linux](Category:Linux "wikilink")
