---
layout: post
title: "Use Specific version of rails before creating  a new app"
date: 2013-06-27 01:56
comments: true
categories: Rails
status: publish
type: post
published: true
---

You want to develop with the latest version of Rails but you have an existing application that
uses an older version that you are not ready to bring up to date. What do you do?

By default gem will keep older versions of installed gems until you tell it not to. To see what you have installed:

    $ gem list --local

    [...]

    rails (4.0.0.beta1, 3.2.13)

To use a specific version in your application add a line like this to the bottom of your config/environment.rb file

    RAILS_GEM_VERSION = '3.2.13'

That should just work.

You can get rid of old versions of gems with this command:

    $ gem cleanup

If you remove an old version by mistake you can always reinstall it with this gem command:

    $ sudo gem install rails --version 3.2.12

When you are ready to move your application to the current version of rails then remove the line from environment.rb and bring your application files up to date with:

    $ rake rails:update

Now, let's say you have installed the current version of Rails (say, 4.0.0.beta1) but you need to build an application that uses an older version. According to 'rails --help' there is no way to specify a version to use. It turns out that there is a hidden option available that does this:

    $ rails _3.2.13_ myapp


--

Manu S Ajith

[@manusajith](http://twitter.com/manusajith/ "Twitter") | [Git](http://github.com/manusajith/ "Twitter") |  
