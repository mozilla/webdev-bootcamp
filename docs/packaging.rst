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
Let's say we want to update Django to 1.2.5.
We already have Django
setup in our ``requirements/prod.txt``
as well as a submodule of our vendor
directory.

``prod.txt``::

  -e git://github.com/django/django@36c82ac8#egg=django

So we're on ``a85fe4dddc4b133de289`` which is Django 1.2.3.

We want to go to ``b8ac1085778ebed65`` which is Django 1.2.5.::

  $ pwd
  /home/fubert/project/playdoh
  $ git pull
  $ vi requirements/prod.txt

prod.txt::

  -e git://github.com/django/django@b8ac1085778ebed65#egg=django

Save and quit, puts us back on the command line.::

  $ git submodule update --recursive
  $ cd vendor
  $ git pull
  $ git submodule update --recursive
  $ cd src/django
  $ git checkout b8ac1085778ebed65
  $ cd ../..
  $ git add src/django
  $ git commit -m"Bug 1235 Upgrading to Django 1.2.5"
  $ git push origin master
  $ cd ../..
  $ git add vendor requirements/prod.txt
  $ git commit -m"Bug 1235 Upgrading to Django 1.2.5"
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
