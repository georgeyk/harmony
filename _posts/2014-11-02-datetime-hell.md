---
layout: post
title:  "Localized date/time hell"
date:   2014-11-02 17:00:45
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

**Notes**

Actually, the use of pytz and datetime might still be broken if you use datetime.now, take a look:

{% highlight python %}
>>> from datetime import datetime
>>> from pytz import timezone
>>> tz = timezone('America/Sao_Paulo')
>>> datetime.now().strftime('%Y-%m-%d %H:%M:%S %Z%z')
'2014-11-05 19:10:55 '
>>> tz.localize(datetime.now()).strftime('%Y-%m-%d %H:%M:%S %Z%z')
'2014-11-05 19:11:12 BRST-0200'
{% endhighlight %}

As you notice, there is no date and time convertion, just a setting of timezones. And it is also
true if we use datetime.utcnow.

One way to workaround this is to use [python-dateutil][dateutil] or [Arrow][arrow]:

{% highlight python %}
>>> from dateutil.tz import gettz
>>> from datetime import datetime
>>> import arrow
>>> tz = gettz('America/Sao_Paulo')
>>> datetime.now(tz).strftime('%Y-%m-%d %H:%M:%S %Z%z')
'2014-11-05 19:19:56 BRST-0200'
>>> datetime.utcnow().strftime('%Y-%m-%d %H:%M:%S %Z%z')
'2014-11-05 21:20:58 '
>>> arrow.now('America/Sao_Paulo').strftime('%Y-%m-%d %H:%M:%S %Z%z')
'2014-11-05 19:26:03 BRST-0200'
{% endhighlight %}

o/

[datetime]: https://docs.python.org/2.7/library/datetime.html#tzinfo-objects
[pytz]: http://pytz.sourceforge.net/#localized-times-and-date-arithmetic
[dateutil]: https://labix.org/python-dateutil
[arrow]: http://crsmithdev.com/arrow/
