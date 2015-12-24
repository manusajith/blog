---
layout: post
title: Install Adobe Flash Player 11.2 on Fedora 17/16, CentOS/RHEL 6.2/5.8
tags:
- adobe
- browser
- centos
- chrome
- codingarena
- fedora
- firefox
- flash
- flash player
- google
- internet
- Internet
- Linux
- manu
- neo
- ubuntu
- youtube
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'no'
  _edit_last: '1'
  tumblrize_post-type: regular
  tumblrize_post-group: manusajith.tumblr.com
---

##Install Adobe YUM Repository RPM package##

Adobe Repository 32-bit x86
    rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux

Adobe Repository 64-bit x86_64
    rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
    rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux

##Update Repositories##

    yum check-update

###Install Adobe Flash Player 11.2 on Fedora 17/16/15/14/13/12, CentOS 6.2/6.1/6 and Red Hat (RHEL) 6.2/6.1/6###

Fedora 17/16/15/14/13/12, CentOS 6 and Red Hat (RHEL) 6 32-bit and 64-bit version
yum install flash-plugin nspluginwrapper alsa-plugins-pulseaudio libcurl

Install Adobe Flash Player 11.2 on CentOS 5.8 and Red Hat (RHEL) 5.8
CentOS and Red Hat 32-bit and 64-bit version

    yum groupinstall "Sound and Video"
    yum install flash-plugin nspluginwrapper curl


<a href="http://facebook.com/manusajith">Manu</a>

<a href="http://www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>