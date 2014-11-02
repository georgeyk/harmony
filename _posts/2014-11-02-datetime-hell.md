---
layout: post
title:  "Localized date/time hell"
date:   2014-11-02 17:00:45
description: Just a sample post to show some of the typography elements supported from harmony theme.
categories:
- blog
- en
- datetime
- python
--- 

Once in a while we still need to work with localized dates instead of UTC and almost everytime we
have bad surprises.

This time it was no different, but an example will demonstrate this better than words:

{% highlight python %}
>>> from datetime import datetime
>>> from pytz import timezone

>>> tz = timezone('America/Sao_Paulo')
>>> datetime(2014, 11, 2, tzinfo=tz)
datetime.datetime(2014, 11, 2, 0, 0, tzinfo=<DstTzInfo 'America/Sao_Paulo' LMT-1 day, 20:54:00 STD>)
>>> tz.localize(datetime(2014, 11, 2)
datetime.datetime(2014, 11, 2, 0, 0, tzinfo=<DstTzInfo 'America/Sao_Paulo' BRST-1 day, 22:00:00 DST>)

{% endhighlight %}

Did you see that (LMT/BRST) ? WTF those dates are not equals ? Which one is correct ?

The answer is that the standard [datetime][datetime] module does not work with every timezones and
we are advised to use [pytz][pytz] when working with localized date and times. 

(So the second way is the correct one)

That hurts!

o/

[datetime]: https://docs.python.org/2.7/library/datetime.html#tzinfo-objects
[pytz]: http://pytz.sourceforge.net/#localized-times-and-date-arithmetic
