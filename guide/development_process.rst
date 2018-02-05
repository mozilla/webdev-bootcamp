Development Process
===================

While the details vary, there is a general framework for the development
process at Mozilla which describes how a change goes from an idea in someone's
head to deployed code on a production webserver. This document attempts to
describe that process.

Filing a Bug
------------

The first thing that happens is that a bug is filed in the bug tracker of
choice for the project. A well-written bug includes:

- A description of the issue, possibly including steps to reproduce or a link
  to an example if the issue is a problem with the project.
- Information or links to any conversation that is happening outside of the
  bug, such as a mailing list thread.
- If appropriate, a specified mentor to help new contributors work on the
  issue.

Depending on the project, the bug may be triaged and assigned a priority and/or
milestone, or it may be added to another system for tracking work, such as a
kanban board.

Working on the Bug
------------------

Either someone will voluntarily take a bug, or, in the case of projects with
assigned developers actively working on them, it will be assigned to a
developer.

The process of fixing a bug involves:

- Marking the bug as assigned to you so that others do not work on the bug at
  the same time.
- Creating a feature branch in your version control system to isolate your work
  from the work of others.
- Making the changes required to fix the issue or implement the new feature.
- Writing automated tests to ensure that your changes work as expected, as well
  as manually testing on your personal development instance of the project.
- Submitting your changes for review by another developer on the project, and
  updating your changes in response to the review.
- Merging your feature branch back into the main branch used for development.

Git and GitHub
^^^^^^^^^^^^^^

For projects using Git and GitHub (which is most Webdev projects), the process
can be explained in more detail:

- On GitHub, ensure you have `forked the repository`_ for your project to your
  own account and have added it as a `remote`_ to your repository.
- Identify the main development branch for your project. This is usually the
  ``master`` branch.
- Make sure the current branch is the development branch and create a new
  branch off of it for your feature.
- Once your work is committed and ready for review, `push the branch`_ to your
  fork on GitHub and `submit a pull request`_.
- If you know who should review your change, add a comment to your pull request
  with their ``@Username`` in it and ask for a review (often abbreviated as
  ``r?``).

.. seealso::

   :doc:`/reference/glossary`
      A glossary of specialized terms used within Webdev, including some
      abbreviations used for code review, such as ``r?``, ``r+``, and ``r-``.

   `GitHub Flow <https://guides.github.com/introduction/flow/>`_
      A process for branching, reviewing, and merging code that is very similar
      to the process above.

.. _forked the repository: https://help.github.com/articles/fork-a-repo
.. _remote: https://help.github.com/articles/about-remote-repositories
.. _push the branch: https://help.github.com/articles/pushing-to-a-remote
.. _submit a pull request: https://help.github.com/articles/using-pull-requests

Testing and Deployment
----------------------

Once a change is merged into the codebase, it needs to be tested on an actual
server and then deployed to production. Typically the lead developer on a
project will handle this process and let you know if any effort on your end is
required.

A bug is usually marked as resolved when it is merged into the codebase.
Depending on the issue tracker being used, the bug may also be marked as
verified once the changes are tested and approved.

Next steps
----------

At this point you should have all the information and tools you need to make
your first contribution to Mozilla! Once you've submitted your work and gotten
it merged, it's time to celebrate: you've earned it!

As you continue to contribute, you may want to check out the
:doc:`/reference/index` to find generally-useful information for contributors
of all levels.

Good luck!
