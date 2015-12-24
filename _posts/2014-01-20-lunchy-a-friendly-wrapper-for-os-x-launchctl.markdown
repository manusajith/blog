---
layout: post
title: "lunchy: A friendly wrapper for OS X launchctl"
date: 2014-01-20 22:27:17 +0530
comments: true
categories: Ruby Gem OSX
tags: Ruby Gem
---

If you run OS X, you’ve probably encountered some frustration with Apple’s launchctl command line options when starting, stopping, and restarting your launchd daemons. Whereas most things Apple are minimalist, launchctl options are quite verbose.

<!--more -->

For example, how many times have you installed a Homebrew package only to get met with something like:

If this is your first install, automatically load on login with:

    cp /usr/local/Cellar/mongodb/1.6.5-x86_64/org.mongodb.mongod.plist ~/Library/LaunchAgents
    launchctl load -w ~/Library/LaunchAgents/org.mongodb.mongod.plist


If this is an upgrade and you already have the org.mongodb.mongod.plist loaded:

    launchctl unload -w ~/Library/LaunchAgents/org.mongodb.mongod.plist
    cp /usr/local/Cellar/mongodb/1.6.5-x86_64/org.mongodb.mongod.plist ~/Library/LaunchAgents
    launchctl load -w ~/Library/LaunchAgents/org.mongodb.mongod.plist

Or start it manually:

    mongod run --config /usr/local/Cellar/mongodb/1.6.5-x86_64/mongod.conf

So to crank up Mongo you want me to pass that entire path to launchctl?

Lunchy – "Start your agents and go to lunch"
Thank goodness there’s Lunchy from Mike Perham. Lunchy simplifies the command line interface to launchctl. To get started, install the gem:

gem install lunchy
Now we can list all of our agents with ls

    $lunchy ls
      com.adobe.AAM.Updater-1.0
      com.adobe.CS5ServiceManager
      com.apple.FTMonitor
      com.apple.apsd-ft
      com.apple.imagent
      com.apple.marcoagent
      com.bjango.istatlocal
      com.embercode.TVShowsHelper
      com.github.dotjs
      com.google.keystone.agent
      com.mysql.mysqld
      com.wacom.pentablet
      net.culater.SIMBL.Agent
      net.sourceforge.tvshows
      org.mongodb.mongod
      org.postgresql.postgres
      ws.agile.1PasswordAgent
… and start MongoDB with

    lunchy start mongo
    
To see the full range of options, just type lunchy with no arguments:

Supported commands:

    ls [pattern]       Show the list of installed agents, with optional [pattern] filter
    start [pattern]    Start the first agent matching [pattern]
    stop [pattern]     Stop the first agent matching [pattern]
    restart [pattern]  Stop and start the first agent matching [pattern]
    status [pattern]   Show the PID and label for all agents, with optional [pattern] filter
Got an idea to improve upon Lunchy? Go ahead and fork the project

[Source on GitHub](http://github.com/mperham/lunchy)

[Source: TheChangelog](http://thechangelog.com/lunchy-a-friendly-wrapper-for-launchctl/)
