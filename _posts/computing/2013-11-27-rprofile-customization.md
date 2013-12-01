---
layout: post
published: true
title: .Rprofile Customization
tagline: ''
category: 'computing'
tags: [r]
---


In case you want to specific your CRAN repo and change installed package type. Edit the file in `~/.Rprofile`

{% highlight r %}
local({
r <- getOption("repos")
r["CRAN"] <- "http://cran.us.r-project.org"
options(repos = r)
})

local({
platform = .Platform
platform$pkgType = "mac.binary"
unlockBinding(".Platform", asNamespace("base"))
assign(".Platform", platform, inherits=TRUE)
lockBinding(".Platform", asNamespace("base"))
options(pkgType = "mac.binary")
})
{% endhighlight %}    