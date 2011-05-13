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


.. _python:

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


.. _PEP8: http://www.python.org/dev/peps/pep-0008/
.. _check.py: https://github.com/jbalogh/check.py
.. _Pocoo: http://www.pocoo.org/internal/styleguide/

Django
------

Follow :ref:`python`.  There are a few things in Django that will make your
life easier:

Use ``resolve('myurl')`` and ``{{ url('myurl') }}`` when linking to internal
URLs.
This will handle hosts, relative host names, changed end points for you.  It
will also noticably break so dead-links don't linger in your code.

.. highlight:: jinja

Indentation within templates should be handled as such::

  {% if indenting %}
    <p>This is how it's done</p>
  {% endif %}

Playdoh
~~~~~~~

New web-apps should be spawned from Playdoh_ and existing ones should follow
the spirit of Playdoh_.  Playdoh_ collects lessons that several Mozilla Django
projects have learned and wraps them into a single Django project template.

In the future,
much of Playdoh_'s
moving parts (Middleware, filters, etc) will be moved into a separate
library so these features won't be lost.

.. _Playdoh: https://github.com/mozilla/playdoh

Javascript
----------

* Use JSLint_.
* Write QUnit tests when possible.
* Do not write JS in the HTML.
* Prefer single quotes over double.

.. _JSLint: http://www.jslint.com/

HTML
----

* Use the HTML5
* Make sure your code validates.
* No CSS or JS in the HTML
* Be semantic
* Use doublequotes for attributes::

    <a href="#">Good</a>
    <a href='#'>Less Good</a>
