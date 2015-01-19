---
layout: post
title: Switching between pythons using pyenv on OSX
tagline: 
category: computing
tags: [python, osx]
last_modified: 
---

### Installation

From [pyenv](https://github.com/yyuu/pyenv),

> pyenv lets you easily switch between multiple versions of Python

As always, I recommend to use [homebrew](http://brew.sh) to install `pyenv`.
Assuming that you have already installed homebrew, to install `pyenv`, you need

```bash
brew update
brew install pyenv
```

This will also create a hidden folder under your user directory `~/.pyenv`. In most cases,
you don't have look at this directory.

To enable `pyenv`, put the following into your `~/.bash_profile` or `~/.zshrc` if you are using [zsh](http://www.zsh.org). I strongly recommend zsh. Try to install it via homebrew and give it a try.

```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

To enable shell completions, also add this to your shell config file

```bash
# for bash shell
if [[ -f /usr/local/opt/pyenv/completions/pyenv.bash ]]; then
    source /usr/local/opt/pyenv/completions/pyenv.bash
fi

# for zsh shell
if [[ -f /usr/local/opt/pyenv/completions/pyenv.zsh ]]; then
    source /usr/local/opt/pyenv/completions/pyenv.zsh
fi
```


Resetting your shell terminal, and check if `pyenv` runs. To list supported versions of python

```bash
pyenv install --list
```

For academic use, I strongly recommend `anaconda3`, e.g., `anaconda3-2.1.0`. (Also, give a try to `pypy3`)
Installation is a piece of cake.

```bash
pyenv install anaconda3-2.1.0
```

It may take some time for the installation process to finish.


To show available versions of python

```bash
pyenv versions
```
You should see `system` and  `anaconda3-2.1.0`. System python is the version of python first found along the `PATH` variable.



<hr>

### Switch between

- To activate `anaconda3-2.1.0` in the current terminal session.

```bash
pyenv shell anaconda3-2.1.0
# check python version
python -V
# Python 3.4.1 :: Anaconda 2.1.0 (x86_64)
```

- If you want to use `anaconda3-2.1.0` every time you visit a particular project directory, say `~/project`. 

```bash
# unset the shell specific version
pyenv shell --unset
# go to the project directory
cd ~/project
pyenv local anaconda3-2.1.0
# check python version
python -V
# Python 3.4.1 :: Anaconda 2.1.0 (x86_64)
```

Note: you run `python -V` outside `project`, you will see the system python.


- To use `anaconda3-2.1.0` globally, run `pyenv global anaconda3-2.1.0`. But I don't recommend this.

<hr>

### Remove pyenv

If you really don't like `pyenv` and want to remove all traces of `pyenv` files. Just remove `pyenv` from homebrew and remove the `~/.pyenv` directory. It will do the job. Of course, you have to also undo the changes made to the `~/.bashrc_profile` or `~/.zshrc` files.