---
layout: post
title: Simple Server monitoring Shell Script
tags:
- apache
- bash
- centos
- Coding
- codingarena
- internet
- Linux
- manu
- neo
- security
- server
- server status
- shell
- shell script
- site
- status
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  snapEdIT: '1'
  snapLI: s:41:"a:1:{i:0;a:1:{s:10:"SNAPformat";s:0:"";}}";
  snap_isAutoPosted: '1'
  snapTR: s:43:"a:1:{i:0;a:1:{s:11:"isPrePosted";s:1:"1";}}";
  dsq_thread_id: '927376920'
---
##A simple shell script to monitor whether your server is running or not.##
This script should be made to run on some other server, because when your server goes down all the scripts will stop executing too, so there is no point in running the script on the same server.

<!--more-->

###Create a new file###
    vim servermonitor.sh

Add the following contents to the file and save it.

    if curl -s --head http://codingarena.in | grep "200 OK" > /dev/null
        then
		    echo "Server running" > /dev/null
    else
		    echo " Server Down at" `date` > $PWD/time
  	    curl -s --head http://codingarena.in/ > $PWD/failed
		    mail -s "Server Down " neo@codingarena.in < $PWD/failed
    fi

Next make the file executable by:

    chmod u+x servermonitor.sh

Now add a new entry to your cron job to execute the script for the interval of time specified.

I am going to run it every 5 minutes, so
    crontab -e

and add
    */5 * * * * /path_to_file/monitor.sh

Save the file.

And thats it. whenever your server goes down you will get a mail alert.

Fork the code at <a href="https://github.com/manusajith/simple_server_monitor"> Github</a> | <a href="https://bitbucket.org/manusajith/simple_server_monitor">Bitbucket</a>


<a href="http://facebook.com/manusajith">Manu</a>

<a href="http://www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>
