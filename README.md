
django-appengine-setup
======================

## Introduction

``django-appengine-setup`` is a simple script for generating django-nonrel
projects for Google App Engine. It will download all the dependencies and store
them in the ``lib/py`` directory. It will also patch ``djangoappengine`` to add
``lib/py`` to the list of python system paths.

## Installation

Just clone the repo as if it were your project, and run ``./manage
createproject``. This will delete .git repository folder, initialize
an new repository and continue with the project setup.

Here is an example for project named *myproject* with AppEngine installed to
*/opt/google-appengine-python*:

```bash
$ git clone https://github.com/novopl/google-appengine-setup myproject
$ cd myproject
$ ./manage createproject myproject /opt/google-appengine-python
```

## Managing the project

``manage.py`` will require changing the ``PATH`` environment variable, so
you have to either modify it yourself, or you can use the ``manage`` script
to execute all ``manage.py`` commands. If the given command is not directly
implemented by ``manage`` it will be passed to ``manage.py`` but it will
also setup up correct ``PATH`` beforehand. The only thing to do is to replace
each call to ``./manage.py`` by a call to ``manage``

Here are a few examples of how this can be used:

```bash
# Initialize database
$ ./manage syncdb

# Deploy the application in the AppEngine cloud
$ ./manage deploy
```

## Supported commands

There is a number of commands implemented by ``manage``, any command not
matching the below is passed to ``manage.py`` directly.

Command list:

* ``syncdb``, ``collectstatic``, etc -- django commands passed directly to
``manage.py``,

* ``createproject`` -- initializes a new project in the folder, will create a
fresh django-appengine boilerplate, in the current folder, nested  under
project name,

* clean -- recursively removes all temporary files from the project directory
(\*~, \*.pyc, \*swp),

* ``downloaddeps`` -- installs django-nonrel with all dependencies,

* ``setupproject`` -- creates django project, tweaks it and creates virtualenv
with google_appengine reference,

* ``pylib`` -- installs a python library to project's virtualenv using pip and
copies it to lip/py,

* ``deploy`` -- uploads the app to the App Engine.
