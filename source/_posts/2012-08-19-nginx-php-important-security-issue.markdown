---
layout: post
title: Nginx & PHP important security issue
tags:
- apache
- codingarena
- config
- configuration
- internet
- Internet
- IT
- Linux
- manu
- neo
- nginx
- php
- security
- Security
- server
- site
- ubuntu
- web
- web server
- Website
- website
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'no'
  _edit_last: '1'
  _wp_old_slug: ''
---

A critical security issue has recently been pointed out on servers that run Nginx and PHP via FastCGI. The issue allows anyone to execute their own PHP code on the system, I don't think I have to remind you of the consequences this could have. I will attempt to provide a simple explanation of the issue and more importantly how to fix it.

##What is the issue? ##
I would like to begin by discussing the nature of the problem: it is not caused by Nginx itself - it is not a bug or a security breach in itself. Actually, it is the way that people usually configure Nginx FastCGI options to work with PHP, and how PHP reacts to that configuration. Pretty much everyone adopts the same configuration without being aware of the issue.

The issue itself can be understood simply, then I will explain why PHP behaves that way. Most dynamic websites allow for a reason or another uploading of files. Say, I'm running a forum-based community, users can upload images to use as personal photo or avatar. The photo gets uploaded and you get the following URL:

<code><em>http://myforum.com/uploads/photo1234.jpg</em></code>

The breach consists in appending an additional path element to the URL, making it end in .php:

<code><em>http://myforum.com/uploads/photo1234.jpg/anything.php</em></code>

Under certain conditions (and unfortunately with default settings), your photo1234.jpg gets processed as PHP file. So you could upload a PHP script renamed as .jpg, upload the image, then execute the script on the server.

If you want to know instantly if your server is vulnerable to this attack, there is a simple way to know. Find a regular file on your server, such as

<code><em>http://myforum.com/robots.txt.</em></code>

Examine the HTTP headers of the response:
    HTTP/1.1 200 OK
    Server: nginx/0.7.64
    Date: Wed, 26 May 2010 10:56:01 GMT
    Content-Type: text/plain
    Content-Length: 43
    (...)

Now add /test.php after the URL:

<code><em> http://myforum.com/robots.txt/test.php: </em></code>

    HTTP/1.1 200 OK
    Server: nginx/0.7.64
    Date: Wed, 26 May 2010 10:56:01 GMT
    Content-Type: text/plain
    Content-Length: 43
    (...)
    X-Powered-By: PHP/5.2.3

The X-Powered-By header was added by PHP which shows that the file was processed by PHP. Now visit that URL http://myforum.com/robots.txt/test.php in your web browser. What do you see:

- do you see the robots.txt file ? if so, your server is vulnerable.
- do you see an error page (403, 404, 500, 502...) or just a simple message "No input file specified" ? if so, your server is not affected by the problem.

##Why does this happen?##
There are two main reasons why this happens. First let's have a look at the data Nginx transmits to PHP.
A regular FastCGI/PHP configuration would be as follows:

    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
    fastcgi_param SCRIPT_FILENAME <em>/var/www/vhosts/myforum.com/httpdocs$fastcgi_script_name;</em>
    fastcgi_param PATH_INFO $fastcgi_script_name;

When requesting an URL like<em> http://myforum.com/uploads/photo1234.jpg/anything.php</em> to Nginx, here is the data that gets sent:

    fastcgi_param SCRIPT_FILENAME <em>/var/www/vhosts/myforum.com/httpdocs/uploads/photo1234.jpg/anything.php;</em>
    fastcgi_param PATH_INFO /robots.txt/test.php;

So far, no problem. PHP is supposed to load a file anything.php, in the directory <em>/var/www/vhosts/myforum.com/httpdocs/uploads/photo1234.jpg/.</em> Naturally, this directory should not exist, and anything.php shouldn't exist either, so we should be getting a 404 error.
However, that's where the problem comes in. The PHP option cgi.fix_pathinfo, when enabled (and it is usually enabled by default) will transform these two parameters. The SCRIPT_FILENAME becomes <em>/var/www/vhosts/myforum.com/httpdocs/uploads/photo1234.jpg,</em> which means the .jpg file actually becomes the request filename, and it gets treated as PHP. And PATH_INFO becomes /anything.php. The original purpose of this option was to allow such kind of URLs: index.php/param1/param2/...
But when combined with Nginx, this turns into a major issue.


##How do I fix it?##
Well, the simplest thing you can do is open up your php.ini configuration file, and insert this directive in the main section:
    cgi.fix_pathinfo=0
Then restart PHP-FPM or whatever FastCGI manager you're using.

Unfortunately in some cases that is not possible a solution, since perhaps other scripts on your server make the most of this option. So you could do mainly employ two different solutions on the Nginx side.

First, you could check that the requested URI actually exists, before passing the request via FastCGI:

    location \.php$ {
        if (!-f $request_filename) {
            return 404;
        }
        fastcgi_pass 127.0.0.1:9000;
        [...]
    }

This solution is efficient and a few of us Nginx+PHP have retained it.
Otherwise, if you think it's too consuming in terms of resources, you could check the URI to meet the following requirements:
- if the URI contains a dot, then a slash (example: image.jpg/...)
- if the URI ends with ".php" (example: image.jpg/test.php)
- then return a 403 error.
    location ~ \..*/.*\.php$ {
        return 403;
    }
    location ~ \.php$ {
        fastcgi_pass 127.0.0.1:9000;
        ...
    }

Alternatively, you could make sure that PHP is only enabled in certain directories, where file uploads are not allowed:
    location ~ ^/(scripts|sources|src)/.*\.php$ {
        fastcgi_pass 127.0.0.1:9000;
        ...
    }

<a href="http://facebook.com/manusajth">Manu</a>

<a href="www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>
