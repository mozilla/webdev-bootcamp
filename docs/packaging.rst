Packaging and Dependency Management
===================================

Python projects can incur
a number of dependencies.
``pip`` can be handy, but we've had better luck with distributing a ``vendor``
library.

For the basics, read `Zamboni packaging`_ as well as Playdoh_'s docs.

.. _`Zamboni packaging`: http://jbalogh.github.com/zamboni/topics/packages/
.. _Playdoh: http://mozilla.github.com/playdoh/packages/

Updating a Library
------------------
Let's say we want to update Django to 1.3.
We already have Django
setup in our ``requirements/prod.txt``
as well as a submodule of our vendor
directory.

``prod.txt``::

  -e git://github.com/django/django@1.2.5#egg=django

So we're on Django 1.2.5.  We want to go to Django 1.3.  We edit
``prod.txt``::

  -e git://github.com/django/django@1.3#egg=django

Save and quit, puts us back on the command line.::

  $ git submodule update --recursive
  $ pushd vendor
  $ git pull
  $ git submodule update --recursive
  $ pushd src/django
  $ git checkout origin/1.3
  $ popd
  $ git add src/django
  $ git commit -m"Bug 1235 Upgrading to Django 1.3"
  $ git push origin master
  $ popd
  $ git add vendor requirements/prod.txt
  $ git commit -m"Bug 1235 Upgrading to Django 1.3"
  $ git push origin master

Now other developers can pick up your changes into their
`virtualenv`
and IT can pickup your changes in `vendor` and push out to
the web heads.

Upgrading Libraries
-------------------
To keep up-to-date, one should occassionally do::

  pip install --upgrade -r requirements/compiled.txt
  pushd vendor
  git submodule --update --init
  popd

This will refresh the libraries you've installed with their
latest tagged version.

Todo
----
Write tools to automate this.
