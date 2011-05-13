Git and Github
==============

Unless you have a good reason
you should be using ``git`` and Github_
for version control.
One notable exception is
many of our projects
rely on
SVN for localizers.
We'll be attempting to
phase that out.

If you don't know ``git`` or haven't used it in a team, the best wa

github.com/mozilla
------------------
New projects for Mozilla websites should
start in the `Mozilla account`_.

Contact ``jbalogh`` or ``jsocol`` to be
added to the webdev group of the
Mozilla account.

.. _`Mozilla account`: https://github.com/mozilla
.. _Github: https://github.com/

Working on projects
-------------------
In order to work on a project:

* Fork it into your own account (do not develop directly in ``origin``)
* Make a branch for your work
* Submit a pull request for review
* Merge your commit into ``master`` which should track the ``origin/master``
* ``git push``
* Place a link to the commit (as it appears in the origin repository) in the
  relevent bug.

Commit Messsages
~~~~~~~~~~~~~~~~

* Follow these guidelines_.
* Should begin with a 50 character summary, with details if needed below.
* Should contain ``bug 1234`` somewhere in the summary.

.. _guidelines: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

Keeping master in sync
~~~~~~~~~~~~~~~~~~~~~~

You will want to keep your local ``master`` branch in sync.  Typically you
will rebase your branches with your ``master`` and ultimately you will push
your ``master`` to ``origin/master``.

Let's assume you've defined your ``origin`` remote propperly in github.  E.g.
for Zamboni_. ::

    origin	git@github.com:jbalogh/zamboni.git

.. _Zamboni: https://github.com/jbalogh/zamboni

You will want your ``.gitconfig`` to have the following::

    [branch "master"]
        remote = jbalogh
        merge = master
        rebase = true

Making life easier
------------------

Git Tools
~~~~~~~~~
In order to make life easier we maintain a repository_ of ``git-tools``.  These
are shell scripts or python scripts that commit all kinds of magic.

.. _repository: https://github.com/davedash/git-tools

Here's a sampling:

* `git here` will tell you the name of your branch, this is an excellent
  building block
* ``git bugbranch $BUGNUM`` will copy your current branch to an appropriately
  named bug branch.  This uses the :ref:`Bugzilla API bugzilla-api`.
* ``git compare``
  with the appropriate ``git.config`` settings
  will give you a
  Github_ compare URL
  for your branch (you'll need to push to Github_ on your own).
* ``git url``
  with the appropriate ``git.config`` settings
  gives you the last commit's URL on Github_.

Put these in your path and then fork and make your own tools and share.

Oh My Zsh
~~~~~~~~~

`Oh My Zsh <https://github.com/robbyrussell/oh-my-zsh>` is an excellent
collection of zshell scripts that can make your `zsh` environment amazing.  It
includes a collection of plugins, including ones for ``git`` and Github_.

Some of these overlap with ``git-tools``.  Additionally by using Oh My Zsh you
can easily display your current branch and it's dirtiness on your prompt.

Here is my prompt::

    dash@awesomepants in ~/Projects/bootcamp/the_code/docs
    (bootcamp) ±                                                    on master!

Note:

* ``bootcamp`` is my active `virtualenv`.
* ``±`` signifies that I'm in a ``git`` repository.
* ``master`` is the branch I am in.
* ``!`` indicates that there are uncommitted things in my branch.


Development Process
-------------------

See :ref:`bug-life`

Looking at someone's code
~~~~~~~~~~~~~~~~~~~~~~~~~
Sometimes you need to run someone elses code locally.  If they've given you a
pull request, or a commit hash this is what you need to do to see there code::

    git add remote davedash git@github.com:davedash/zamboni.git
    git fetch davedash
    git co davedash/branch

Note:

* The above assumes that someone else was me.
* The first line defines a
  "remote".  A remote is simply an alias to a repository.
* The second line fetches all my commit hashes that you don't already have.
  Usually this is just branches, and commits, but in theory it can be
  anything.
* In the third line I can check out your branch.  If you just gave me a commit
  hash I would do ``git co $COMMIT_HASH``.

Git resources
-------------

* http://help.github.com/ explains a lot of ``git`` details as they relate to
  Github_.
* ProGit_ is written by one of the Github developers.

.. _ProGit: http://progit.org/book/
