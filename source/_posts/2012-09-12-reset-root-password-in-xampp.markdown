---
layout: post
title: Reset root password in XAMPP
tags:
- apache
- Coding
- coding
- codingarena
- database
- hacking
- Linux
- manu
- mysql
- neo
- password
- reset
- root
- security
- Security
- server
- ubuntu
- website
- xampp
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'no'
  _edit_last: '1'
  _wp_old_slug: ''
  dsq_thread_id: '915233157'
---

In case you forgot your root password for mysql and phpmyadmin

<!--more-->

Go to your xampp\mysql\bin\ folder

Edit my.ini and insert
    skip-grant-tables
below [mysqld]

Restart MySQL

Set new password for your root user by running
    UPDATE mysql.user SET Password=PASSWORD('new_password') WHERE User='root'
in phpMyAdmin in the mysql database (or just leave it like this if MySQL cannot be accessed from remote hosts)

<a href="http://facebook.com/manusajith">Manu</a>

<a href="http://www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>