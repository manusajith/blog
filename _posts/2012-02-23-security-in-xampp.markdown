---
layout: post
title: Security in XAMPP
date: 2012-02-23
tags:
- codingarena
- manu
- neo
- security
- site
- web
- Website
- website
- xampp
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
XAMPP is not meant for production use but only for developers in a development environment. XAMPP is configured is to be as open as possible and to allow the web developer anything he/she wants. For development environments this is great but in a production environment it could be fatal.
<!--more-->
Here a list of missing security in XAMPP:
<ul>
	<li>The MySQL administrator (root) has no password.</li>
	<li>The MySQL daemon is accessible via network.</li>
	<li>phpMyAdmin is accessible via network.</li>
	<li>The XAMPP demopage is accessible via network.</li>
	<li>The default users of Mercury and FileZilla are known.</li>
</ul>
All points can be a huge security risk. Especially if XAMPP is accessible via network and people outside your LAN. It can also help to use a firewall or a (NAT-) router. In case of a router or firewall, your pc is normally not accessible via network. It is up to you to fix these problems. As a small help there is the "XAMPP Security console".

Please secure XAMPP before publishing anything online. A firewall or an external router are only sufficient for low levels of security. For slightly more security, you can run the "XAMPP Security console" and assign passwords.

If you want have your XAMPP accessible from the internet, you should go to the following URI which can fix some problems:
<a href="http://localhost/security/">http://localhost/security/</a>

With the security console you can set a password for the MySQL user "root" and phpMyAdmin. You can also enable a authentication for the XAMPP demopages.

This web based tool does not fix any additional security issues! Especially the FileZilla FTP server and the Mercury mail server you must secure yourself. If you don't need these servers, don't start them. A server which is not started, is very secure!
