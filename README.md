
django-appengine-setup
======================

## Introduction

``django-appengine-setup`` is a simple script for generating django-nonrel
projects for AppEngine. It will download all the dependencies and store
them in the ``lib/py`` directory. It will also patch ``djangoappengine`` to add
``lib/py`` to the list of python system paths.

## Installation

Just clone the repo as if it were your project, and run ``./icanhaz
initproject``. This will remove the ``.git`` folder created by ``git clone``
thus leaving you with a fresh project directory.

Here is an example for project named *myproject* with AppEngine installed to
*/opt/google-appengine-python*:

```bash
$ git clone https://github.com/novopl/google-appengine-setup myproject
$ cd myproject
$ ./icanhaz initproject myproject /opt/google-appengine-python
```

## Managing the project

``manage.py`` will require changing the ``PATH`` environment variable, so
you have to either modify it yourself, or you can use the ``icanhaz`` script
to execute all ``manage.py`` commands. If the given command is not directly
implemented by ``icanhaz`` it will be passed to ``manage.py`` but it will
also setup up correct ``PATH`` beforehand. The only thing to do is to replace
each call to ``./manage.py`` by a call to ``icanhaz``

Here are a few examples of how this can be used:

```bash
# Initialize database
$ ./icanhaz syncdb

# Deploy the application in the AppEngine cloud
$ ./icanhaz deploy
```

## Extra commands

There are currently two extra commands implemented by ``icanhaz``. The already
mentioned ``initproject`` and ``clean``. The latter will recursively remove all
temporary files from the project directory (\*~, \*.pyc, \*swp).

Also there is a shortcut command ``devsrv`` which will clean the project of
temporary files, collect all static and run the server. This is equivalent
to calling ``clean``, ``static``, ``runserver`` in a row.
