---
layout: post
title:  Format Json in command line
date:   2014-10-22 18:12:00
categories:
- blog
- python
- json
---

Just a little trick that might be handy:

{% highlight bash %}
$ alias jsonfmt="python -m json.tool"
$ echo '{"foo": "bar"}' | jsonfmt
{
    "foo": "bar"
}
{% endhighlight %}

The alias creation is optional.
