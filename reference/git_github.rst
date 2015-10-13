Git and Github
==============

This document describes some best practices for using Git and Github.

Best practises
--------------
- Create a separate pull request for each bug. If you have multiple commits in one pull request, squash them into one.
- If you are working with multiple bugs at a time, make sure you create a separate branches for each bug.
- If you need to make changes to the commit, perhaps after feedback, amend the original commit and comment in the pull request what you've changed.  Don't create a new pull request or commit.
- Include  the bug number in your commit & pull request title. If possible  follow this style -`Some text description (bug XXXXXXX)`.
- Don't work on an assigned bug. If you see the bug assignee hasn’t responded for a while (two weeks), then ask for permission if you can work on that bug.
- For frontend pull requests, attach screenshots if relevant.
- Put a link to the PR in the bug as a comment.

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

Owners and the Mozilla Github Organization
------------------------------------------
See the `Github page on wiki.mozilla.org <https://wiki.mozilla.org/Github>`_
for information on the Mozilla organization on Github or anything that requires
owner access for the organization.
