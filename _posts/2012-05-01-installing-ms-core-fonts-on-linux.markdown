---
layout: post
title: Installing  MS Core Fonts on Linux
tags:
- codingarena
- Linux
- manu
- neo
- redhat
- ubuntu
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _wp_old_slug: ''
---

Download the MS Core Fonts Smart Package File

    wget http://corefonts.sourceforge.net/msttcorefonts-2.0-1.spec

Make sure that the rpm-build and cabextract packages are installed:
    yum install rpm-build cabextract

Build the Core Fonts package:
    rpmbuild -ba msttcorefonts-2.0-1.spec

Install the Core Fonts package:
    rpm -Uvh /usr/src/redhat/RPMS/noarch/msttcorefonts-2.0-1.noarch.rpm


<a href="http://facebook.com/manusajith">Manu</a>

<a href="http://www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>
