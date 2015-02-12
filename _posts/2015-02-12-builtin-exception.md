---
layout: post
title:  "python 3 and undefined name for builtins"
date:   2015-02-12 21:20:45
categories:
- blog
- en
- builtin
- python
- python3
---

I was testing something using python3x when I realize that flake8/pep8 always warn me about an
"[W802] undefined name".

Very annoying, to fix that, create a *~/.config/pep8*:


{% highlight ini %}
[pep8]
builtins = _
{% endhighlight %}

o/

[datetime]: https://docs.python.org/2.7/library/datetime.html#tzinfo-objects
[pytz]: http://pytz.sourceforge.net/#localized-times-and-date-arithmetic
[dateutil]: https://labix.org/python-dateutil
[arrow]: http://crsmithdev.com/arrow/
