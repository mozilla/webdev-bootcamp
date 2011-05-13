.. Webdev Bootcamp documentation master file, created by
   sphinx-quickstart on Thu May  5 14:21:14 2011.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Development Process
===================

This document
outlines the development process
for most projects.
**Not every** project
follows this -
notably *Socorro* and *Elmo*.
Check with your team lead or manager
for clarification
and then fork this.

.. index:: release cycle

Release Cycles
--------------

Teams work on 1, 2 or 3-week release cycles.
Ultimately teams want a
continuous development process,
where code can be
developed and placed in
production immediately.

.. index:: bugs, bugs;cycle, milestones
.. _bug-life:

A Bugs Life
-----------
* Most of our work is encapsulated in Bugzilla_.
* Bugs represent tasks (bugs or enhancements).
* A developer lead will typically group the bugs into milestones.
    * Each milestone represent a release.
    * All work done on a project belong in that milestone.
* A developer assigned to a bug will typically:
    * make a "bug branch" in ``git``
    * make code changes
    * commit the code changes
    * push them to a personal GitHub_ repository
    * request a review (``r?``):
            * In bugzilla
            * in IRC
            * over email
            * via GitHub_'s pull request system
                * ``http://github.com/davedash/project/compare/mybugbranch``
                  let you see differences between your work and the
                  ``origin``'s ``master``
    * After a positive review (``r+``) code will be merged into ``master`` and
      pushed to origin.
    * Most projects avoid ``merge`` commits unless they are necessary.
    * The bug is marked fixed and a comment to the GitHub_ commit is left in
      the bug.
* QA will verify all bugs that have been marked fixed.


.. _Bugzilla: https://bugzilla.mozilla.org/
.. _Github: https://github.com/

.. index:: QA

QA
--

QA will verify that bugs are fixed.
If you are working on a bug that does not need
QA verification mark it with ``[qa-]`` in the
whiteboard status.

QA will re-open a bug if they feel it's not complete.
They will file
new bugs if regressions are found within the
current milestone.

.. index:: deployment

Deployment
----------

Deployment varies heavily by product.
A typical flux project will
branch ``master`` into ``prod``
and tag the release with the milestone.

It will then deploy anything in ``prod``.

A typical push consists of:

* Branching and tagging.
* Notifying the ``l10n`` volunteers.
* Filing an IT request (a "push bug").
* Including an etherpad of special instructions if needed.
* Upon QA and Dev approval code is pushed to production
* QA verifies production is working properly
* Hotfixes are made if needed
* Or a rollback happens.

We want a "one button" push process that automates the above steps.
