How to Code
===========

In general, follow the languages established best practices, and fill
in the gaps where there are holes.


.. index:: code;guidelines

General Guidelines
------------------

* *Style matters*

  How code is aligned matters, because code is reviewed, edited, and
  public. Code that is uneasy to read does not align with the spirit
  of open source.

* *Be consistent*

  If you do something a certain way, be able to justify it. Don't mix
  `camelCase` with `underscore_words` unless you have good reason.

* *Follow code around you*

  If you don't know what you're doing try to follow what others have
  done.


.. index:: code;testing

Testing
^^^^^^^

In languages and frameworks that provide easy test-ability, *write
tests!*

Go for 80% or more coverage, especially in the following areas:

* privacy - e.g. test that private things are private
* heavily used code - e.g. landing pages, library level code
* re-opened bugs

Tests last longer than code, as they tend to define the products'
functionality. They are valuable because they allow us to quickly
make changes without fear of hindering functionality.

The other half of testing is continuous integration. We should be
running our tests at every check in and be able to say with certainty
that the code is correct to the best of our knowledge. See
:ref:`ci-chapter`.


.. index:: code;python coding style

.. _python:

Python
------

We do what others in the python community have established:

* We follow PEP8_.
* We test using check.py_ which combines `pep8.py` and `pyflakes`.
* We follow Pocoo_'s extensions of PEP8_ as they are well thought out.


Import Statements
^^^^^^^^^^^^^^^^^

We expand on PEP8_'s suggestions for import statements.  These greatly improve 
ones ability to ascertain what is and isn't available in a given file.

Import one module per import statement::

    import os
    import sys

not::

    import os, sys

Separate imports into groups with a line of whitespace: 
standard library; Django (or framework); third-party; and local imports::

    import os
    import sys

    from django.conf import settings

    import pyquery

    from myapp import models, views


Alphabetize your imports, it will make your code easier to scan.  See how terrible this is::

    import cows
    import kittens
    import bears

A simple sort::

    import bears
    import cows
    import kittens

Imports on top, ``from``-imports below::

    import x
    import y
    import z
    from bears import pandas
    from xylophone import bar
    from zoos import lions

That's loads easier to read than::

    from bears import pandas
    import x
    from xylophone import bar
    import y
    import z
    from zoos import lions


Lastly, when importing things into your namespace from a package use an alphabetized
``CONSTANT``, ``Class``, ``var`` order::

    from models import DATE, TIME, Dog, Kitteh, upload_pets


If possible though, it may be easier to import the entire package, especially for methods 
as it help answers the question, "where did ``you`` come from?"

Bad::

    from foo import you


    def my_code():
        you()  # wait, is this defined in this file?


Good::

    import foo


    def my_code():
        foo.you()  # oh you...


Whitespace matters
^^^^^^^^^^^^^^^^^^

* Use 4 spaces, not 2---it increases legibility considerably.
* Never use tabs---history has shown that we cannot handle them.

Use single quotes unless double (or triple) quotes would be an improvement::

    'this is good'

    'this\'s bad'

    "this's good"

    "this is inconsistent, but ok"

    """this's sometimes "necessary"."""

    '''nobody really does this'''


.. _PEP8: http://www.python.org/dev/peps/pep-0008/
.. _check.py: https://github.com/jbalogh/check
.. _Pocoo: http://www.pocoo.org/internal/styleguide/


.. index:: code;django coding style

Django
------

Follow :ref:`python`. There are a few things in Django that will make
your life easier:

Use ``resolve('myurl')`` and ``{{ url('myurl') }}`` when linking to
internal URLs. This will handle hosts, relative host names, changed
end points for you. It will also noticeably break so dead-links don't
linger in your code.

.. highlight:: jinja

Indentation within templates should be handled as such::

    {% if indenting %}
      <p>This is how it's done</p>
    {% endif %}


.. index:: playdoh

Playdoh
^^^^^^^

New web-apps should be spawned from Playdoh_ and existing ones should
follow the spirit of Playdoh_. Playdoh_ collects lessons that several
Mozilla Django projects have learned and wraps them into a single
Django project template.

In the future, much of Playdoh_'s moving parts (Middleware, filters,
etc) will be moved into a separate library so these features won't be
lost.

See :ref:`packaging`.

.. _Playdoh: https://github.com/mozilla/playdoh

.. index:: code;javascript coding style

Javascript
----------

See :ref:`js-style`.


.. index:: code;html5 coding style

HTML
----

* Use the HTML5
* Make sure your code validates
* No CSS or JS in the HTML
* Be semantic
* Use doublequotes for attributes::

      <a href="#">Good</a>
      <a href='#'>Less Good</a>


.. todo::

   The previous list compiles to weird html where the list is a bunch
   of separate lists.
