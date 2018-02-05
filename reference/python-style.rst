Python Style Guide
==================

This document is a brief set of guidelines for writing Python code for Mozilla
Webdev projects. Individual projects may override these rules; make sure you
know the standards for your project!

General Guidelines
------------------
- Follow PEP8_.
- Follow Pocoo_'s extensions to PEP8, although these are a little less strictly
  enforced across Mozilla projects.
- Check your code against a linting tool. flake8_ is highly recommended for
  this.

.. _PEP8: https://www.python.org/dev/peps/pep-0008/
.. _flake8: https://flake8.readthedocs.io/
.. _Pocoo: https://www.pocoo.org/internal/styleguide/

Import Statements
-----------------

We expand on PEP8_'s suggestions for import statements.

Import one module per import statement::

    import os
    import sys

not::

    import os, sys

Separate imports into groups with a line of whitespace: standard library;
third-party; and local imports::

    import os
    import sys

    from django.conf import settings

    import pyquery

    from myapp import models, views


Alphabetize your imports, it will make your code easier to scan. See how
terrible this is::

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


Lastly, when importing things into your namespace from a package use an
alphabetized ``CONSTANT``, ``Class``, ``var`` order::

    from models import DATE, TIME, Dog, Kitteh, upload_pets


If possible though, it may be easier to import the entire package, especially
for methods as it help answers the question, "where did ``you`` come from?"

Bad::

    from foo import you


    def my_code():
        you()  # wait, is this defined in this file?


Good::

    import foo


    def my_code():
        foo.you()  # oh you...

.. seealso::

   `baked <https://pypi.python.org/pypi/baked>`_
      A tool for automatically checking the import order rules listed above.


Whitespace matters
------------------

* Use 4 spaces, not 2---it increases legibility considerably.
* Never use tabs---history has shown that we cannot handle them.

Use single quotes unless double (or triple) quotes would be an improvement::

    'this is good'

    'this\'s bad'

    "this's good"

    "this is inconsistent, but ok"

    """this's sometimes "necessary"."""

    '''nobody really does this'''

To continue a new line use a ```()``` not ```\```.

Indenting code should be done in one of two ways: a hanging indent, or 4 space
indent on the next line.

Good, using hanging indent. Note that the next line is lined up with the
previous line delimiter::

    log.msg('Something long log message and some vars: {0}, {1}'
            .format(variable_a, variable_b))

Good using 4 spaces::

    accounts = PaymentAccounts.objects.filter(
        accounts__provider__type=2,
        something_else=True
    )

    # A more compact alternative.
    accounts = PaymentAccounts.objects.filter(
        accounts__provider__type=2, something_else=True)

    accounts = (PaymentAccounts.objects
        .filter(accounts__provider__type=2)
        .exclude(something_else=False)
    )

Remember that comprehensibility is the goal here. If following one of the rules
above would result in less readable code, don't follow it!
