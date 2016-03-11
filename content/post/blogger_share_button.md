+++
comments = true
date = 2011-08-25T00:00:00Z
title = "Blogger share button does not work, not visible"
+++

If google share button on blogger does not work with older templates, then add foll piece of css onto ur design template -
{{< highlight css >}}
.post-share-buttons a
{
position: relative;
display: inline-block;
}
{{< /highlight >}}
