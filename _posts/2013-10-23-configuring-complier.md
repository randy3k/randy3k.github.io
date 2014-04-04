---
layout: post
category : computing
title: Configuring complier for R 3.0.x on OSX 10.9 Mavericks
tagline: ""
tags : [r, osx, mavericks]
last_modified: 2014-2-12
---

{: .alert .alert-warning}
**Warning [2014-2-12]**: Most packages are now compatible with `libc++`, changing to `libstdc++` may cause problems for some packages.

On 10.9, the default complier is `clang` with `libc++` library. Many old c++ files may not be compatible with it. Hence some R packages cannot be complied from source. There are 2 solutions.

    1. change the complier to GNU gcc complier.
    2. an easier solution, but it doesn't work for all packages

### 1. GNC gcc complier

First of all, install <a href="http://brew.sh">Homebrew</a>, then install `gcc47` and `gfortran`.

    brew install gcc47
    brew install gfortran

Then edit `~/.R/Makevars`

    CC=/usr/local/bin/gcc-4.7
    CXX=/usr/local/bin/g++-4.7
    FC=/usr/local/bin/gfortran

### 2. An easier solution
Edit `~/.R/Makevars` and add

    CXXFLAGS=-stdlib=libstdc++

But it doesn't fix all problems.

###Test if it works<

You should be able to compile R packages from source now. If the package is installed, it means that you have already changed your complier. As `clang` with `libc++` fails to compile this package.

 
    install.packages("SuppDists", type="source")


Happy R coding~