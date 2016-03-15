+++
comments = true
date = 2012-01-19T00:00:00Z
title = "NPM behind firewall"
description = "Help npm navigate when you are within a corporate firewall."
+++

If you are behind a corporate firewall and want to use [npm](https://www.npmjs.com/) , then you need to configure with foll options.
{{< highlight bash >}}
#npm config set registry http://registry.npmjs.org/
#npm config set proxy http://<my proxy>  
{{< /highlight >}}
