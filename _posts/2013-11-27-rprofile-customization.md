---
layout: post
published: true
title: .Rprofile Customization
tagline: ''
category: 'computing'
tags: [r]
last_modified: 2014-2-12
---


This is my .Rprofile.

{% highlight r %}
# hard code the US repo for CRAN
local({
    r <- getOption("repos")
    r["CRAN"] <- "http://cran.us.r-project.org"
    options(repos = r)
    options(help_type="html")
})

# for color in vanilla R
if (Sys.getenv('TERM') == "xterm-256color"){
    library(colorout)
    setOutputColors256(normal = 20, number = 20, negnum=27,
                       string = 34, const = 214,
                       stderror = 1, warn=9, error=1, verbose=FALSE)
}
{% endhighlight %}    