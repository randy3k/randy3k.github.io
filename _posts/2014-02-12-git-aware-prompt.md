---
layout: post
title: 'Git aware prompt'
tagline: 
category: computing
tags: [git]
last_modified: 2014-8-19
---

I love using git via commands. And it is very often that I have to run `git status` or `git branch` to check if I am on the right branch or I am doing anything correct. Git aware prompt displays the current branch and status of the current directory.

The code was originated from [here](http://bytebaker.com/2012/01/09/show-git-information-in-your-prompt/) but I have made significant amount of changes, for example, adding color support and some bugs fixing.


![](/assets/images/git.png)


To use this, add the following to your `.bashrc` and restart your terminal!

{% gist 1ff38257f4aaff87f3c7 %}