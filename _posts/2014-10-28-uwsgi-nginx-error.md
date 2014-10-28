---
layout: post
title: "The request of death: uWSGI + nginx + buffer sizes"
date: 2014-10-28 18:20:45
categories:
- blog
- en
- bug
- nginx
- uwsgi
---

There was a very strange issue at work: the client was receiving an http 502 status in a certain
page, and he was the only one getting this error (really, just one) and we were not able to reproduce
this behavior.

By analyzing the logs, we saw uWSGI crashing in that situation and then the 502 status was generated.
In the mean time we found that the bug did not happen when the cookies are cleared.

I got stuck for a moment when some coworker mentioned the cookie size limit.
After some investigation, we found out that:

- [uWSGI][uwsgi] allocates 4k by default for request headers
- [Nginx][nginx] allocates 4k or 8k for response reads (depends on platform)
- uWSGI will log this as "invalid request block size (xxx)"


So we increase the "buffer-size" parameter in uWSGI to 8k and the problem seems to be solved.
And we also are able to debug this problem without having the application crash.

I hope this helps someone because this was a very annoying bug!
o/


[uwsgi]: http://uwsgi-docs.readthedocs.org/en/latest/ThingsToKnow.html
[nginx]: http://nginx.org/en/docs/http/ngx_http_uwsgi_module.html#uwsgi_buffer_size
