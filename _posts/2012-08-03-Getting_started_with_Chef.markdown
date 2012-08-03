---
layout: post 
title: Getting started with Chef
---

#### Cookbooks

#### Restrict use specific platforms

    %w{ ubuntu debian fedora centos redhat freebsd openbsd macosx }.each do |os|
      supports os
    end

#### Installing packages

    package "apache2"
