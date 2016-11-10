+++
date = "2016-11-09T17:42:21-04:00"
title = "Getting Setup for Python Development on Mac OS X"
description = "Set up your Mac for easy Python development"
tags = [ "python", "mac" ]
categories = [ "tech" ]

+++

This is a short guide to get properly set up with Python, virtual environments
and git on your Mac (I'm on 10.10).  Heavily inspired by [these](https://hackercodex.com/guide/mac-osx-mavericks-10.9-configuration/)
great [tutorials](https://hackercodex.com/guide/python-development-environment-on-mac-osx/).


## Initial Setup

First install [Homebrew](http://brew.sh/).  It's a great package manager for
OS X and we'll use it to install Python (and keep it updated in the future).

In a terminal, enter:

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


## Install Python

If all went well with the Homebrew installation, we can now use it to install
Python.  While Macs come with Python installed already, it's a better
practice to install a fresh version outside the OS.  It's good to install both
Python 2 and Python 3 although if you know you're only going to use one for all
your development, feel free to just install that one.

```sh
# Install python 2.x
brew install python

# Install python 3.x
brew install python3
```


## Version Control: Install Git

If you're planning on using `git` (if you're not, you should be) and don't
already have it installed, you can also install via Homebrew.

```sh
brew install git
```

I don't cover `git` in this post (yet) but there's a ton of good documentation
out there on how to get started with it.  Initially, just take a look at the
[official docs](https://git-scm.com/doc) if you're just getting started.


## Virtual Environments

Virtual environments allow you to create isolated environments on your
computer where you can install whatever packages you'd like and not have them
interfere with global packages (and vice versa) or other virtual environments.

I would say they are mandatory for Python development so download the below
and learn how to use them!

You can read more about `pip` in the [docs](https://pip.pypa.io/en/stable/) but
essentially it's the defacto Python package manager / installer and pretty
simple to use.  In case you're curious, Homebrew installed `pip` when it
installed `python` so it should be on your machine, ready to use.

```sh
# First download virtualenv, the main package to create and manage
# virtual environments for Python
pip install virtualenv

# Next install some extra tooling that makes creating and managing
# projects even easier
pip install virtualenvwrapper
```


## Environmental Variables in Virtual Environments

This step is optional but if you're going to be setting any configurations or
storing API ids and secrets in environmental variables, I recommend also
installing  `autoenv`. Again, I highly recommend you read the
docs(https://github.com/kennethreitz/autoenv), but this will essentially allow
you to store environmental variables in `.env` files within your virtual
environments and when you enter those environments, those variables will be
set.

```sh
brew install autoenv
echo "source $(brew --prefix autoenv)/activate.sh" >> ~/.bash_profile
```


## Setting Up Virtual Environments

First, you probably should read the `virtualenv` [docs](https://virtualenv.pypa.io/en/stable/)
and `virtualenvwrapper` [docs](https://virtualenvwrapper.readthedocs.io/en/latest/install.html).

You need to set some locations for where you want to store your virtual
environment source (the Python packages and such that you install) and the
actual project folder and files.  Do this via some additional variables in
`~/.bash_profile` or `~/.bashrc`.

Feel free to change the `code` folder and that path to wherever you want to
store your code.  This directory should be created if it doesn't already exist.

```sh
# Settings for python virtualenvwrapper
export WORKON_HOME=$HOME/virtualenvs  # virtualenv source / packages
export PROJECT_HOME=$HOME/code  # project code directory
source /usr/local/bin/virtualenvwrapper.sh  # path to shell script
```

Again, read the documentation, it's well worth it.


## Restricting `pip` to Virtual Environments

There will definitely be times when you think you're in a virtual environment
and you want to install a package within that environment only but then lo and
behold you realize you just installed something globally.

To prevent such muck ups, it's wise to add a little safety check. This is
definitely optional but I find it very helpful to (1) keep me from installing
anything globally that I didn't mean to and (2) let me know when a virtual
environment isn't activated (and I thought it was).

Go to your base directory and in either `.bash_profile` or `.bashrc`, add the
following:

```sh
# Only allow pip commands if within a virtual environment
export PIP_REQUIRE_VIRTUALENV=true
```

So what if you actually do want to install something at the global level?  You
can just set `PIP_REQUIRE_VIRTUALENV` to an empty string.  To make life
easier, you can create a shortcut for that, also within `.bash_profile` or
`.bashrc`.

```sh
# Provide alias `gpip` to install python packages outside a virtualenv
gpip(){
   PIP_REQUIRE_VIRTUALENV="" pip "$@"
}
```

Now, for example, `gpip install virtualenv` would install the package globally
outside a virtual environment.

You should know run the following to make sure everything we've added to
`.bash_profile` (or equivalent) is run.

```sh
source ~/.bash_profile
```


## Creating a Project and Virtual Environment

We use commands from `virtualenvwrapper` to create new Python projects. The
`mkproject` command is super useful because it does several things at once:

  1. Make the virtual environment directory
  2. Make a project directory
  3. Move into that project directory
  4. Activate the virtual environment

Sweet!

Also, note the `-p` argument we specify to use Python3 within the environment.
This is super important if you're going to be coding in and using Python3.

```sh
# Create virtualenv project with Python3
mkproject -p python3 mycoolproject
```

You're all set!  You can now install any packages you need and start developing
projects, all in the inner sanctum of the virtual environment.

For instance, just `pip install django` and you're ready to start hacking away
on a new web project.

If you ever need to get back into that virtual environment, all you do is type
`workon mycoolproject` and you'll be transported to your code folder with an
activated virtualenv.

Hope this was useful and let me know if you have any issues.
