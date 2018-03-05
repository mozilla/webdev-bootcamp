.. _js-style:

JS Style Guide
==============

First and Foremost
------------------

**ALWAYS** use JSHint_ on your code.

.. Note::

   JSHint may warn about some features of Node.js that aren't present in your
   typical browser implementation of JavaScript. These can be safely ignored.
   You can ignore some JSHint warnings permanently with a `.jshintrc` file.

.. _JSHint: http://www.jshint.com/


Variable Formatting:
--------------------

.. code-block:: javascript

    // Classes: CapitalizedWords
    var MyClass = ...

    // Variables and Functions: camelCase
    var myVariable = ...

    // Constants: UPPER_CASE_WITH_UNDERSCORES
    const MY_CONST = ...


Indentation
~~~~~~~~~~~

4-space indents (no tabs).

For our projects, always assign var on a newline, not comma separated:

.. code-block:: javascript

    // Bad
    var a = 1,
        b = 2,
        c = 3;

    // Good
    var a = 1;
    var b = 2;
    var c = 3;


Use ``[]`` to assign a new array, not ``new Array()``.

Use ``{}`` for new objects, as well.

The array literal ``[]`` can be used with either a single line or multiple
lines, depending how easy it is to read:

.. code-block:: javascript

    // Okay on a single line
    var stuff = [1, 2, 3];

    // Never on a single line, multiple only
    var longerStuff = [
        'some longer stuff',
        'other longer stuff'
    ];


Never assign multiple variables on the same line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example of what not to do:

.. code-block:: javascript

    var a = 1, b = 'foo', c = 'don\'t do this';


DO NOT line up variable names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For consistency, don't do this:

.. code-block:: javascript

    var wut    = true;
    var boohoo = false;


Semi-colons
-----------

**Use them.**

Even though JavaScript can use automatic semicolon insertion (ASI), you should
still use semi-colons to be consistent with the rest of the codebase.


Conditionals and Loops
----------------------

.. code-block:: javascript

    // Bad
    if (something) doStuff()

    // Good
    if (something) {
        doStuff();
    }


Space after keyword, and space before curly
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: javascript

    // Bad
    if(bad){
        // This is bad
    }

    // Good
    if (something) {
        // This is better
    }


Functions
---------

Named Functions
~~~~~~~~~~~~~~~

You should assign functions to named symbols, like so:

.. code-block:: javascript

    var updateOnClick = function() { ... };

Here, the function above is known as ``updateOnClick``. The same can be done
with objects. In the example below, ``someObject.updateOnClick`` is the
function:

.. code-block:: javascript

    var someObject = {
        updateOnClick: function() { ... }
    };

If you're passing a nontrivial function as an argument, you should name it to
avoid obscuring what it's supposed to do.

Don't do this:

.. code-block:: javascript

    obj.forEach(function(item) {
        // A large anonymous function with dozens of lines of code.
        // This makes it hard to understand what the function does
        // without reading through it entirely.
    });

Instead, do the following:

.. code-block:: javascript

    var doMagic = function(item) { ... };

    obj.forEach(doMagic);

Here, it is easy to see that ``doMagic`` gets called for each object.


Whitespacing Functions
~~~~~~~~~~~~~~~~~~~~~~

Do not put a space between "function" and the opening parenthesis. Do put a
space after the closing parenthesis and before the opening curly brace:

.. code-block:: javascript

    var method = function(argOne, argTwo) {
        // Do something
    };


Anonymous Functions
~~~~~~~~~~~~~~~~~~~

Anonymous functions are fine if they have a small amount of code in them. See
the :ref:`named-functions` section for more information about inferred function
names for anonymous functions.


Operators
---------

Always use strict equality (``===``).

The only exception to this rule is when testing for null and undefined.

Example:

.. code-block:: javascript

    if (value != null) {
        // This is an exception to the rule. Usually you'd use !==
    }


Quotes
------

Always use single quotes: ``'not double'``

There is only one exception: ``"don't escape single quotes in strings; use double quotes instead"``


Comments
--------

For Node.js functions, always provide a clear comment in this format:

.. code-block:: javascript

    /* Briefly explains what this does
     * Expects: whatever parameters
     * Returns: whatever it returns
     */


If your comment is really long, use the format mentioned above (``/* ... */``).
Otherwise make short comments like so:

.. code-block:: javascript

    // This is a short comment that ends in a period.


Ternaries
---------

Avoid using the ternary operator (``(condition) ? (true) : (false)``).

If using the ternary operator makes a line particularly complex, or would
require using multiple lines, don't use it:

.. code-block:: javascript

    // Bad
    var foo = (user.lastLogin > new Date().getTime() - 16000) ? user.lastLogin - 24000 : 'wut';

    // Good
    return user.isLoggedIn ? 'yay' : 'boo';


General Good Practices
----------------------

* Don't repeat yourself! If you see yourself repeating something that could be
  a constant, refactor it as a single constant declaration at the top of the
  file.
* Try caching your regular expressions (regex) by declaring them as constants.
* Always check for truthiness:

  .. code-block:: javascript

      // Bad
      if (blah !== false) { ... }

      // Good
      if (blah) { ... }

* If one line in your code is really long, you should probably refactor it. If
  this isn't possible, try breaking it up into multiple lines.
* Try to keep within the 80-column limit (but if you go a bit past it's not a
  big deal). Indent the subsequent lines one indent (2-spaces) in.
* If it looks too clever, it probably is, so just make it simple.
