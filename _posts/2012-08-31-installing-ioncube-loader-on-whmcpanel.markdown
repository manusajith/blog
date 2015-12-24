---
layout: post
title: Installing ioncube loader on WHM/cPanel
tags:
- apache
- centos
- coding
- codingarena
- cpanel
- e-commerce
- google
- ion-cube
- ioncube
- Linux
- manu
- neo
- php
- server
- site map
- web
- website
- whm
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'no'
  _edit_last: '1'
  _wp_old_slug: ''
  dsq_thread_id: ''
---

Tutorial on Installing Ioncube Loader on WHM/cPanel

<!--more-->

##Download It##
    wget http://downloads.ioncube.com/loader_download /ioncube_loaders_lin_x86.tar.gz
    tar zfx ioncube_loaders_lin_x86.tar.gz
    mv ioncube /usr/local

Find PHP.ini
    php -i | grep php.ini

Edit your php.ini
    pico /usr/local/lib/php.ini or nano /usr/local/lib/php.ini

Add Extension to PHP.ini
    zend_extension=/usr/local/ioncube/ioncube_loader_lin_5.3.so

Restart Apache
    service httpd restart

Check
    php -v
    PHP 5.3.10 (cli) (built: Aug 10 2009 05:47:14)
    Copyright (c) 1997-2009 The PHP Group
    Zend Engine v2.2.0, Copyright (c) 1998-2009 Zend Technologies
    Copyright (c) 2002-2009, by ionCube Ltd.
    with Suhosin v0.9.27, Copyright (c) 2007, by SektionEins GmbH

<a href="http://facebook.com/manusajth">Manu</a>

<a href="www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>
