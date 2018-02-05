
Git and GitHub
==============

This document describes some tips and tricks for using Git and GitHub.
There are also some best practices for :ref:`best-practices-github`.

Commit Messages
---------------

See `Tim Pope's blog post on git commit messages
<http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html>`_.

Rebasing Commits
----------------

While projects vary in their opinions on whether merge commits should be
avoided or not, it is generally a good idea to rebase a feature branch before
submitting a pull request.

Rebasing allows you to alter a series of commits, changing the history of your
repository. Typically you rebase a branch to:

- Combine smaller commits made during development into larger, logical commits
  that are easier to understand and review, or split up larger commits into
  smaller commits for the same purpose.
- Alter commit messages of previous commits.
- Move a branch to be based on the latest commit of the branch you want to
  merge into and resolve any conflicts that occur.

These changes all make the code review process as well as the merging process
easier, and are recommended for all pull requests.

.. warning:: Rebasing code that has already been pushed to a public or shared
             repository makes it very difficult for others to update their
             local repositories. Only rebase branches that you are absolutely
             sure no one else is using, such as feature branches on your
             personal fork.

.. seealso::

   `Using Git rebase <https://help.github.com/articles/using-git-rebase>`_
      A short guide on how to use the ``git rebase`` command.

Asking for Review
-----------------

When asking someone for a code review, it is recommended to add a new comment
to a pull request using the ``@Username`` syntax. This notifies them via email
that a review has been requested. Adding the ``@Username`` to the pull request
description will **not** send out the notification and thus isn't recommended.

You may also add an attachment to a bug in Bugzilla and paste in the URL for
the pull request as the content. This will cause Bugzilla to link to the pull
request and allow you to set the review bit on the attachment to track the
state of the review in Bugzilla.

Owners and the Mozilla GitHub Organization
------------------------------------------
See the `GitHub page on wiki.mozilla.org <https://wiki.mozilla.org/Github>`_
for information on the Mozilla organization on GitHub or anything that requires
owner access for the organization.
