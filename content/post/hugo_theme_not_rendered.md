+++
date = "2016-03-15T08:04:34+05:30"
description = "Hugo theme not rendered correctly when hosted on a server, whereas `hugo server` works fine."
title = "Hugo theme not rendered correctly"
tags = ["Hugo", "styling", "theme", "css", "garbled"]

+++

You have built your site with Hugo. `hugo server` command renders the site fine. But hosting it on
github pages or your webserver renders it garbled or does not render correctly. If you have hit the above
behavior, you are not alone.

`tl; dr`

The baseurl in config.(yaml|toml) should point to the url on which the site is hosted and not the domain name.
For e.g. if you are hosting the site on github, setting should be
{{< highlight js >}}
baseurl = "http://<your-user-name>.github.io/"
{{< /highlight >}}
and not yourdomain.com

if you are hosting locally or on your own, it should be
{{< highlight js >}}
baseurl = "http://<ip-address>:<port>/"
{{< /highlight >}}

Note the **trailing /** that ends the base url.

The problem is with the base url setting and styling associated with it. Normally most of the themes
have partials(partial html snippets which make up a page) like following below.
{{< gist keshavab 7efd202b851cd6080650 "linenos=inline,hl_lines=11 12 13 14">}}

Ideally, the themes should have used relative indexes instead of absolutely referring urls, since
browsers take care of them. However, most of themes out there refer resources from `Site.BaseURL`.

The reason why this works when run with `hugo server` command is that, Hugo internally replaces the baseurl
with the `localhost:port` to `localhost:1313`(defaults) and hence they are rendered correctly.
