How to Code
===========

In general,
follow the languages established best practices, and
fill in the
gaps
where there are holes.

General Guidelines
------------------
* *Style Matters* how code is aligned matters, because code is reviewed,
  edited, and public.  Code that is uneasy to read does not align with the
  spirit of open source.
* *Be consistent* if you do something a certain way, be able to justify it.
  Don't mix `camelCase` with `underscore_words` unless you have good reason.
* *Follow code around you* if you don't know what you're doing try to follow
  what others have done.

Testing
~~~~~~~
In languages and frameworks that provide easy test-ability, *write tests!*

Go for 80% or more coverage, especially in the following areas:

* privacy - e.g. test that private things are private
* heavily used code - e.g. landing pages, library level code
* re-opened bugs

Tests last longer than code,
as they tend to define the products' functionality.
They are valuable because
they allow us to quickly make changes without
fear of
hindering functionality.

The other half of testing is continuous integration.
We should be running our tests at
every check in and be able to say with
certainty that
the code is correct to the best of our knowledge.
See :ref:`ci`.

Python
------

We do what others do:

* We follow PEP8_.
* We test using check.py_ which combines `pep8.py` and `pyflakes`.
* Pocoo_ has good guidelines as well, let's steal them.

Also, spaces matter:

  * Use 4 spaces, not 2 it increases legibility considerably.
  * Never use tabs, history has shown that we cannot handle them.

Use single quotes unless you need double (or triple) quotes::

    'this is good'

    'this\'s bad'

    "this's good"

    "this is inconsistent, but ok"

    """this's sometimes "necessary"."""

    '''nobody really does this'''

Breaking lines::


Django
------
Playdoh
~~~~~~~
Javascript
----------
HTML
----
CSS
---


    single quotes unless you need double or triple quotes



    django

    templates

    always use {{ url }} for internal links

    indentation within code

    playdoh

    javascript

    jquery

    html

    No CSS/JS in your HTML

* python
    - pep8
    - check.py
    - tests w/ commits
* javascript
   - jslint
   - testing with Qunit and jstestnet (CI)

