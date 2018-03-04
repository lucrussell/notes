---
ID: 734
post_title: Pyenv Quick Reference
author: Luc
post_excerpt: ""
layout: post
permalink: >
  http://lucrussell.com/pyenv-quick-reference/
published: true
post_date: 2018-03-04 12:49:09
---
[Pyenv](https://github.com/pyenv/pyenv) is a tool for easily switching between multiple versions of Python. One way to use the tool is in conjunction with the `pyenv-virtualenv` and `pyenv-virtualenvwrapper` plugins.

Detailed instructions are available [here](https://anil.io/blog/python/pyenv/using-pyenv-to-install-multiple-python-versions-tox/) and [here](http://akbaribrahim.com/managing-multiple-python-versions-with-pyenv/). The following reference is a brief summary of some frequently used commands.


## Install Pyenv, pyenv-virtualenv and pyenv-virtualenvwrapper

    curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash

    git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv

    git clone https://github.com/pyenv/pyenv-virtualenvwrapper.git $(pyenv root)/plugins/pyenv-virtualenvwrapper

Edit your profile (e.g. `~/.bash_profile` or `~/.zshenv`) and add the following, adjusting paths as necessary:

    # Use pyenv for Python version management
    export PYENV_ROOT="$HOME/Dev/.pyenv"
    export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"
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