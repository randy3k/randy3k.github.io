---
layout: post
published: true
title: .Rprofile Customization
tagline: ''
category: 'computing'
tags: [r]
last_modified: 2014-3-29
---


This is my .Rprofile.

{% highlight r %}
# not using user library
# .libPaths("")

# hard code the US repo for CRAN and use HTML to help
local({
    r <- getOption("repos")
    r["CRAN"] <- "http://cran.rstudio.com/"
    options(repos = r)
    options(help_type="html")
})


# using browser for help in R gui
if (.Platform$GUI == "AQUA"){
    local({
        platform = .Platform
        platform$GUI = ""
        unlockBinding(".Platform", asNamespace("base"))
        assign(".Platform", platform, inherits=TRUE)
        lockBinding(".Platform", asNamespace("base"))
    })
}

.First = function(){
    if (.Platform$GUI == "X11" & Sys.getenv("RSTUDIO")==""){
        if ("colorout" %in% rownames(utils::installed.packages())){
            colorout::setOutputColors256(normal = 20, number = 20, negnum=27,
                               string = 34, const = 214,
                               stderror = 1, warn=9, error=1, verbose=FALSE)
        }else if (Sys.getenv("R_colorout")==""){
            Sys.setenv(R_colorout=TRUE)
            library(stats)
            library(utils)
            install.packages("devtools")
            devtools::install_github("randy3k/colorout")
            Sys.setenv(unset="R_colorout")
        }
    }
}

{% endhighlight %}    