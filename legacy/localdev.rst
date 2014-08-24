Developing Locally
==================

For many sites (AMO, SUMO, Input, etc), developing locally is an easy
achievement.

Developing locally allows you to be able to work anywhere without relying on
network connectivity.

.. index::
   single: mac
   single: osx
   pair: git;installation

Homebrew (OS X)
-------------------

Most web developers choose a MacBook Pro as their development machine.
Therefore we recommend Homebrew_. Almost all the required development tools can
be acquired via ``brew``:

* git
* sphinx search
* mysql
* redis
* memcached
* python
* gettext (you'll want the GNU version; the BSD version that comes with OS X
  won't play well with playdoh_)

If you need something that ``brew`` doesn't support, but you could otherwise
compile, you can create your own recipes.

.. _playdoh: https://github.com/mozilla/playdoh

Xcode (OS X)
----------------

You need Apple's Xcode to compile packages. If you're on the Mozilla network (in
the Mountain View office or on OfficeVPN) you can connect to fs2 (``smb://fs2``)
using your LDAP account and find a recent version of Xcode 3 in the "mac"
folder.

You can also get Xcode from http://developer.apple.com/xcode/, if you have an
Apple Developer account. There are currently problems using Homebrew with Xcode
4, so make sure you get a recent version of Xcode 3 if you're downloading it
from Apple's site. You can install Xcode 3 and 4 alongside each other (in
separate folders) if you already use Xcode 4 for other things.

If you're in the Mozilla Mountain View office (or you have VPN access to it via
Mozilla-MV) you can grab a recent, compatible version of Xcode 3 from our
``fs2`` file server by connecting to ``smb://fs2`` as a guest and selecting the
``public`` volume. Xcode 3.2 is in the ``mac`` folder. See more about
:ref:`vpn-info`.

*Note*: If you don't have an Apple Developer account, it might be easier to
simply grab Xcode from the shared volume on ``fs2``. Navigating the Apple
Developer site, especially if your account is a free account, can be a bit of a
maze.


.. _Homebrew: https://github.com/mxcl/homebrew/


Homework
--------

Install Homebrew_ and install ``git``, ``sphinx``, ``mysql``, ``gettext``, and
``python``. You'll need at least these items for most projects.

For gettext, you'll need to ``brew link gettext`` so your system uses the GNU
version of gettext instead of the BSD version Apple provides.
