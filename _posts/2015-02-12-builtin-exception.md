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

Very annoying and I could not find anything to fix that without remove the warning (entirely).

In the meanwhile, I'm importing from the builtins module just to make them happy.
For example:

{% highlight python %}

from builtins import FileNotFoundError

{% endhighlight %}

o/
