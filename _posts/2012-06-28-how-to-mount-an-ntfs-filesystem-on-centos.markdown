---
layout: post
title: How to Mount an NTFS Filesystem on CentOS
tags:
- centos
- codingarena
- file system
- filesystem
- Linux
- manu
- neo
- ntfs
- Security
- ubuntu
- yum
status: publish
type: post
published: true
meta:
  _wp_old_slug: ''
  _edit_last: '1'
  aktt_notify_twitter: 'no'
  dsq_thread_id: '973523991'
---

##Installing required packages##

###Install the following packages###

    yum install fuse fuse-ntfs-3g

If the rpmforge repo is disabled by default,
    yum --enablerepo=rpmforge install fuse fuse-ntfs-3g
    yum install ntfs-3g
    yum install ntfsprogs ntfsprogs-gnomevfs

###Mounting an NTFS filesystem###

Suppose your ntfs filesystem is /dev/sda1 and you are going to mount it on /mymnt/win, do the following.

First, create a mount point.
    mkdir /mymnt/win

Next, edit /etc/fstab as follows. To mount read-only:
    /dev/sda1       /mymnt/win   ntfs-3g  ro,umask=0222,defaults 0 0

To mount read-write:
    /dev/sda1       /mymnt/win   ntfs-3g  rw,umask=0000,defaults 0 0

You can now mount it by running:
    mount /mymnt/win

<a href="http://facebook.com/manusajith">Manu</a>

<a href="http://codingarena.in" title="Codingarena">Codingarena</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>