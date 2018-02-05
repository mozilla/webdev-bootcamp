Glossary
========

At Mozilla Webdev we use a lot of special terms that mean specific, non-obvious
things to those who aren't familiar with them. This document attempts to
define those terms.

.. glossary::

   pull request
   PR
      A term for a request on GitHub to merge some changes into a codebase.
      Pull requests are the primary place where code review happens for GitHub
      projects.

   r?
      Abbreviation for a request to review a piece of code.

   r+
      Abbreviation for passing a code review.

   r+wc
      Abbreviation for passing a code review *with changes*. This means there
      was feedback on things to change during the review, but the requested
      changes are so minor that a subsequent review is not necessary after
      making them.

   r-
      Abbreviation for failing a code review. This usually means that more
      work is needed rather than rejecting the code outright. After the
      requested changes are made, another code review is required.
