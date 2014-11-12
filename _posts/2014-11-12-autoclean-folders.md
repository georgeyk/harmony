---
layout: post
title:  "Automatic cleaning folders"
date:   2014-11-12 17:13:45
categories:
- blog
- en
- linux
- bash
---

I started to test an idea: given a folder (in my case, ~/Downloads), remove everything that is older
than X days.

It's really simple to temporary folders become very messy and get lost in too many files without
remembering which one is important or not.


I put a command like this in my crontab:

{% highlight bash %}

$ find ~/Downloads/* -mtime +30 -exec rm {} \; 2>&1 | xargs -d"\n" -I {} date +"%Y-%m-%d %H:%M:%S: {}" >> ~/deleted.log

{% endhighlight %}

It does not look very nice, but is dead simple:

* find the files that is older than 30 days in Downloads folder
* Remove those files
* Redirect any output to the stdout
* For each line of the output, add a timestamp
* Log everything to ~/deleted.log file

And everything after the find command is optional.

o/
