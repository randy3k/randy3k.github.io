---
layout: post
title: 'Git aware prompt'
tagline: 
category: computing
tags: [git]
last_modified: 
---

I love using Git via commands. And it is very often that I have to run `git status` or `git branch` to check if I am on the right branch or I am doing anything correct. Git aware prompt displays the current branch and status of the current directory.

The code was originated from [here](http://bytebaker.com/2012/01/09/show-git-information-in-your-prompt/) but I have made significant amount of changes, for example, adding color support and some bugs fixing.


<img src="/assets/images/git.png" style="border:1px solid grey">


To use this, add the following to your `.bashrc` and restart your terminal!


{% highlight bash %}
function git-branch-name
{
    echo $(git symbolic-ref HEAD 2>/dev/null | awk -F/ {'print $NF'})
}
function git-dirty {
    st=$(git status 2>/dev/null | tail -n 1)
    if [[ $st != "nothing to commit, working directory clean" ]]
    then
        echo "*"
    fi
}
function git-unpushed {
    brinfo=`git branch -v | grep $(git-branch-name)`
    if [[ $brinfo =~ ("[ahead "([[:digit:]]*)]) ]]
    then
        echo "+${BASH_REMATCH[2]}"
    fi
}
function gitcolor {
    status=$(git status 2>/dev/null | head -n 1)
    if [[ $status == "" ]]
    then
        echo ""
    else
        if [[ $(git-dirty) == "*" ]];
        then
            color="\033[31m"
        else
            color="\033[32m"
        fi
        echo -e "${color}"
    fi
}

function gitify {
    status=$(git status 2>/dev/null | head -n 1)
    if [[ $status == "" ]]
    then
        echo ""
    else
        echo -e " ($(git-branch-name)$(git-dirty)$(git-unpushed))"
    fi
}

export PS1="(\h)-\W\[\$(gitcolor)\]\$(gitify)\[\033[00m\]\$ "

{% endhighlight %}