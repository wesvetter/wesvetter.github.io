---
layout: post
category: posts
title: Rename localhost
date: 2013-07-17 17:45:00
---

If you're doing web development locally, you're probably navigating to
localhost:XXXX a lot. I got annoyed with having to type out "localhost"
all the time so I created a new domain, "lh", that does the same thing. This
way you can type `lh:3000` rather than `localhost:3000`. It's a small optimization,
but a convenient one if you're a web developer.

To make the change, open up a terminal and run:

{% highlight bash %}
$ sudo vim /private/etc/hosts
{% endhighlight %}

(replacing vim with your favorite command line editor, ie. vim, emacs, nano, etc.)

Then add `127.0.0.1 lh` to the end of the file. The result for me looks like:

{% highlight bash %}
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1 localhost
255.255.255.255 broadcasthost
::1             localhost
fe80::1%lo0 localhost
127.0.0.1 lh
{% endhighlight %}


you may need to flush the DNS cache now. On Snow Leopard[[1]](#1), you can do that with:

{% highlight bash %}
$ dscacheutil -flushcache
{% endhighlight %}

Now sit back and bask in the glory of 7 fewer keystrokes.

---

<a id="1"></a>
[1] I know, I know, I'm getting a new laptop soon, jeez.
