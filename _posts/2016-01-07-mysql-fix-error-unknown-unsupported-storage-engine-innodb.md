---
layout: post
title: "How to Fix MySQL [ERROR] Unknown/unsupported storage engine: InnoDB"
date: 2016-01-08 00:48:17 +0530
comments: true
categories: Git
---

After playing around with my MySQL configuration file in my docker container, MySQL was throwing a weird error, and was failing to start.

I checked the error logs and found an entry in the error log.

```
[ERROR] Plugin ‘InnoDB’ init function returned error.
[ERROR] Plugin ‘InnoDB’ registration as a STORAGE ENGINE failed.
[ERROR] Unknown/unsupported storage engine: InnoDB
[ERROR] Aborting

```

After googling and searching SO for a while, I realised that  the solution is to rename or delete some of the log files of InnoDB. In case you are concerned about the data, it would be wise to have a backup of those files, in my case I encountered the error on a fresh docker MariaDB container. Hence I chose to remove the files.

```
rm /var/lib/mysql/ib_logfile0
rm /var/lib/mysql/ib_logfile1
```

and then restart MySQL.

```
root@docker# /etc/init.d/mysql start
Starting MySQL database server: mysqld . ..
Checking for tables which need an upgrade, are corrupt or were not closed cleanly..
root@docker#
```

And thats it, I now have my MySQL server up and running once again.
