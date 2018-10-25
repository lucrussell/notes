---
ID: 734
post_title: Pyenv Quick Reference
author: Luc
post_excerpt: ""
layout: post
permalink: >
  https://lucrussell.com/pyenv-quick-reference/
published: true
post_date: 2017-12-04 12:49:09
---
[TOC]: # "Contents"

# Contents
- [Install Pyenv, pyenv-virtualenv and pyenv-virtualenvwrapper](#install-pyenv-pyenv-virtualenv-and-pyenv-virtualenvwrapper)
    - [Pyenv Installer](#pyenv-installer)
- [Usage](#usage)
    - [List Available Python Versions](#list-available-python-versions)
- [Install a specific version](#install-a-specific-version)
    - [Create A New virtualenv Based on a Specific Python Version](#create-a-new-virtualenv-based-on-a-specific-python-version)
- [Customize pip.conf](#customize-pipconf)
- [Other Useful Commands](#other-useful-commands)



[Pyenv](https://github.com/pyenv/pyenv) is a tool for easily switching between multiple versions of Python. One way to use the tool is in conjunction with the `pyenv-virtualenv` and `pyenv-virtualenvwrapper` plugins.


Detailed instructions are available [here](https://anil.io/blog/python/pyenv/using-pyenv-to-install-multiple-python-versions-tox/) and [here](http://akbaribrahim.com/managing-multiple-python-versions-with-pyenv/). The following reference is a brief summary of some frequently used commands.



## Install Pyenv, pyenv-virtualenv and pyenv-virtualenvwrapper

###  Pyenv Installer
First use the [Pyenv Installer](https://github.com/pyenv/pyenv-installer). The 'Github Way' of installing is easiest.

Edit your profile (i.e. `~/.bash_profile`, `~/.zshenv`, etc) and add the following, adjusting paths as necessary:

    # Use pyenv for Python version management
    export PYENV_ROOT="$HOME/Dev/.pyenv" <--Use your chosen location here
    export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"


Then install the following two plugins:
- [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
- [pyenv-virtualenvwrapper](https://github.com/pyenv/pyenv-virtualenvwrapper)

Edit your profile again, adding the following:

    eval "$(pyenv virtualenv-init -)"
    export WORKON_HOME=$HOME/.virtualenvs
    export PROJECT_HOME=$HOME/Dev
    source /usr/local/bin/virtualenvwrapper.sh
    pyenv virtualenvwrapper

## Usage

### List Available Python Versions

    pyenv install -l

## Install a specific version

    pyenv install 3.6.4

### Create A New virtualenv Based on a Specific Python Version
See the full guide [here](http://docs.python-guide.org/en/latest/dev/virtualenvs).

    pyenv versions
    pyenv shell 3.6.4
    mkvirtualenv --python=`pyenv which python` mynewenv

## Customize pip.conf
You can set a project or virtualenv specific pip.conf by creating one in
$VIRTUAL_ENV/pip.conf when the virtualenv is active:

    $ workon myenv
    $ vi $VIRTUAL_ENV/pip.conf

Add this:

    [global]
    index-url = https://<path_to_a_corporate_repo>

## Other Useful Commands

| Command           | Description |
|-------------------|-------------|
| lsvirtualenv      | List all the virtualenvs |
| echo $WORKON_HOME | Show the directory where virtualenvs are located |
| workon myvirtualenv | Set the current virtualenv to myvirtualenv |
| pyenv global      | Show the global Python version currently in use |
| pyenv versions      | Show which Python versions are installed |
| pyenv global 3.6.4      | Switch to the 3.6.4 version if installed |