Developing Locally
==================

For many sites (AMO, SUMO, Input, etc),
developing locally is an easy achievement.

Developing locally
allows you to be able to work anywhere without relying on
network connectivity or being.

.. index::
   single: mac
   single: osx
   pair: git;installation

Homebrew (Mac OS X)
-------------------

Most web developers choose a MacBook Pro as their development machine.
Therefore we recommend Homebrew_.
Almost all the required development tools can be acquired via ``brew``:

* git
* sphinx search
* mysql
* redis
* memcached
* python

If you need something that ``brew`` doesn't support, but you could otherwise
compile, you can create your own recipes.

*Note*: You need Apple's Xcode to compile packages. If you're on the Mozilla
network (in the Mountain View office or on OfficeVPN) you can connect to fs2
(``smb://fs2``) using your LDAP account and find a recent version of Xcode 3
in the "mac" folder.

You can also get Xcode from http://developer.apple.com/xcode/, if you have an
Apple Developer account. There are currently problems using Homebrew with
Xcode 4, so make sure you get a recent version of Xcode 3 if you're
downloading it from Apple's site.


.. _Homebrew: https://github.com/mxcl/homebrew/


Homework
--------

Install Homebrew_ and
install ``git``, ``sphinx``, ``mysql`` and ``python``.
You'll need at least these items
for most projects.
