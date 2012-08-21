.. index:: git, github

.. _git-chapter:


Git and Github
==============

Unless you have a good reason you should be using ``git`` and GitHub_
for version control. One notable exception is many of our projects
rely on SVN for localizers. We'll be attempting to phase that out.

Git Resources
-------------

If you don't know ``git`` or haven't used it in a team, fear not! There are
lots of awesome sites for git newbies. We recommend:

* Help.Github_ can help you get started with ``git`` regardless of
  your operating system. If you haven't used GitHub_ before, it's the
  perfect crash course. There's also some good info about ``git``
  itself. You can ignore the "deploy" section, as we have our own
  deployment process at Mozilla.
* `Pro Git`_ is probably the best ``git`` resource in existence. It
  covers pretty much everything you'd want to know about ``git``, so
  it's quite lengthy, but it's a great read to get to know the basics
  or to use as a reference. `Pro Git`_ is written by one of the
  developers at GitHub_.
* There's a good `list of git resources on StackOverflow`_. It lists
  tools, tutorials, reference guides, etc. A lot of handy stuff there.

Next time you start a project, use ``git``/GitHub_!  Working on a
project by yourself is a bit different than working with others, but
start with some basic ``git`` commands (clone, branch, merge) and some of 
the more wild stuff (multiple origins, rebasing, etc.) will make more sense.

.. _Help.Github: http://help.github.com/
.. _`Pro Git`: http://progit.org/book/
.. _`list of git resources on StackOverflow`: http://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide

Git Practices at Mozilla
------------------------

* Read about the `git-flow model`_. We work similarly to this at
  Mozilla, except we use ``master`` as our development branch,
  ``prod`` for our production branch, and ``bug-$BUG_NUMBER`` as our
  feature branches. Once you get to know ``git``, understanding how to
  use/manage branches effectively will allow you to keep different bug
  fixes and features in their own branches. This is **really
  awesome**, especially if regressions crop up!
* We use ``git submodule`` for our libraries. This `git submodules explained`_
  article helps you understand how they work.
* We often use ``git rebase`` to combine and fix commits before merging to
  mozilla origin repositories. This helps code reviews and keeps
  commit history clean. GitHub has `a good rebase article`_.

.. _`git-flow model`: http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/
.. _`git submodules explained`: http://longair.net/blog/2010/06/02/git-submodules-explained/
.. _`a good rebase article`: http://help.github.com/rebase/

github.com/mozilla
------------------

New projects for Mozilla websites should start in the `Mozilla
account`_.

Contact ``jsocol``, ``wenzel`` or ``peterbe`` to be added to individual projects
you want to have your way with. They hang out in **#webdev** on IRC,
which is a fine place to ask for access when you start at Mozilla.

.. _`Mozilla account`: https://github.com/mozilla
.. _GitHub: https://github.com/

Service Hooks
~~~~~~~~~~~~~

GitHub has some service hooks that are helpful to Mozilla projects.

* Bugzilla - posts comments on bugzilla when commit messages reference a
  bug by id, and closes bugs when commit message says 'fix' or 'close'
* IRC - announces repository pushes in an irc channel

Contact ``davedash`` or ``wenzel`` to get access parameters for the
hooks.

Working on projects
-------------------
In order to work on a project:

* Fork it into your own account (do not develop directly in ``origin``)
* Make a branch for your work
* Submit a pull request for review
* Merge your commit into ``master`` which should track the
  ``origin/master``
* ``git push``
* Place a link to the commit (as it appears in the origin repository)
  in the relevant bug.

Commit Messages
~~~~~~~~~~~~~~~

* Follow these guidelines_.
* Should begin with a 50 character summary, with details if needed below.
* Should contain ``bug 1234`` somewhere in the summary.

.. _guidelines: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

Keeping master in sync
~~~~~~~~~~~~~~~~~~~~~~

You will want to keep your local ``master`` branch in sync. Typically
you will rebase your branches with your ``master`` and ultimately you
will push your ``master`` to ``origin/master``.

Let's assume you've defined your ``origin`` remote properly in GitHub.
E.g. for Zamboni_. ::

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

**shell**

In order to make life easier we maintain a repository_ of
``git-tools``. These are shell scripts or python scripts that commit
all kinds of magic.

.. _repository: https://github.com/davedash/git-tools

Here's a sampling:

* ``git here`` will tell you the name of your branch, this is an excellent
  building block
* ``git bugbranch $BUGNUM`` will copy your current branch to an
  appropriately named bug branch. This uses the :ref:`Bugzilla API
  <bugzilla-api>`.
* ``git compare`` with the appropriate ``git.config`` settings will
  give you a Github_ compare URL for your branch (you'll need to push
  to Github_ on your own).
* ``git url`` with the appropriate ``git.config`` settings gives you
  the last commit's URL on Github_.

Put these in your path and then fork and make your own tools and share.

**vim**

fugitive.vim_ may very well be the best Git wrapper of all time.

.. _fugitive.vim: https://github.com/tpope/vim-fugitive

Oh My Zsh
~~~~~~~~~

`Oh My Zsh <https://github.com/robbyrussell/oh-my-zsh>` is an
excellent collection of zshell scripts that can make your `zsh`
environment amazing. It includes a collection of plugins, including
ones for ``git`` and Github_.

Some of these overlap with ``git-tools``. Additionally by using Oh My
Zsh you can easily display your current branch and it's dirtiness on
your prompt.

Here is my prompt::

    dash@awesomepants in ~/Projects/bootcamp/the_code/docs
    (bootcamp) ±                                                    on master!

Where:

* ``bootcamp`` is my active `virtualenv`.
* ``±`` signifies that I'm in a ``git`` repository.
* ``master`` is the branch I am in.
* ``!`` indicates that there are uncommitted things in my branch.


Development Process
-------------------

See :ref:`bug-life`

Looking at someone's code
~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes you need to run someone else's code locally. If they've
given you a pull request, or a commit hash this is what you need to do
to see there code::

    git remote add davedash git@github.com:davedash/zamboni.git
    git fetch davedash
    git co davedash/branch

Note:

* The above assumes that someone else was me.
* The first line defines a "remote". A remote is simply an alias to a
  repository.
* The second line fetches all my commit hashes that you don't already
  have. Usually this is just branches, and commits, but in theory it
  can be anything.
* In the third line I can check out your branch. If you just gave me
  a commit hash I would do ``git co $COMMIT_HASH``.
