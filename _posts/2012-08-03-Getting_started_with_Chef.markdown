---
layout: post 
title: Getting started with Chef
---

#### Cookbooks

#### Install Chef Client

*References
<http://wiki.opscode.com/display/chef/Installing+Chef+Client+on+CentOS>*
Installed and works on CentOS 6.2

    sudo rpm -Uvh http://rbel.frameos.org/rbel6
    sudo yum install ruby ruby-devel ruby-ri ruby-rdoc ruby-shadow gcc gcc-c++ automake autoconf make curl dmidecode

    cd /tmp
    curl -O http://production.cf.rubygems.org/rubygems/rubygems-1.8.10.tgz
    tar zxf rubygems-1.8.10.tgz
    cd rubygems-1.8.10
    sudo ruby setup.rb --no-format-executable

    #This command can appear to hang, unless you use the verbose flag.
    sudo gem install chef --no-ri --no-rdoc

#### Restrict use to specific platforms

    %w{ ubuntu debian fedora centos redhat freebsd openbsd macosx }.each do |os|
      supports os
    end

#### Installing packages

    package "apache2"
