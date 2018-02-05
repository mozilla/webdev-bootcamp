.. _css-style:

CSS Style Guide
===============

Terminology
-----------

Just so we all know what we're talking about, a CSS *rule* comprises one or more
*selectors* followed by a *declaration block* consisting of one or more
*declarations*. A declaration comprises a *property* and a *value* (some
properties accept multiple values).

A rule in CSS looks like::

    selector {
        property: value;
    }


The basics (tl;dr)
------------------

* Multi-line rules, not single line.
* Spaces, not tabs.
* Four space indentation.
* Order declarations alphabetically (with some exceptions).
* Use the simplest, least specific selector possible.
* Make meaningful names, not presentational.
* All lowercase for classes and IDs, no camelCase.
* Separate words in classes and IDs with hyphens, not underscores.
* ID selectors are allowed but use them sparingly and appropriately.
* Don't use ``!important``.
* You can use pixels for ``font-size``, but you don't have to.
* Use unitless ``line-height``.
* Group related rules into sections.
* Order sections and rules from general to specific.
* Use Stylus but write it like plain CSS.

General guidelines
------------------

If a length value is ``0``, do not specify units; ``0px`` and ``0in`` are exactly
equal because zero is zero.

Omit leading zeroes in decimal units, e.g. ``.75em``, not ``0.75em``.

When using experimental properties with vendor prefixes, always include the
unprefixed declaration as well, and always last in the list. An exception would
be a strictly vendor-specific property with no standard implementation, like
``-webkit-font-smoothing``.

When declaring gradient backgrounds, you don't need to include the `old Webkit
syntax`_ unless, for some reason, you need to target old versions of Safari.

.. _old Webkit syntax: https://www.webkit.org/blog/175/introducing-css-gradients/

Practice progressive enhancement! Include solid fallback colors for old
browsers that don't support ``rgba()`` or gradients::

    .widget {
        background: #ccc;
        background: linear-gradient(rgba(155, 155, 155, .25), rgba(155, 155, 155, .5));
    }

Hiding content
~~~~~~~~~~~~~~

Consider screen readers when hiding content. Screen readers will not read
content that is ``display: none;`` or ``visibility: hidden;``. Hiding something
visually but not from screen readers requires
`a bit more CSS <https://webaim.org/techniques/css/invisiblecontent/>`_. Be
conscientious when choosing your hiding technique.


Simple selectors
~~~~~~~~~~~~~~~~

Use the least specific selector required to do the job.

Favor classes over IDs.

IDs aren't forbidden, but reserve them for either major blocks (site header,
main nav, etc) or very specific singletons that are truly unique. Hanging styles
from ID selectors can lead to specificity wars requiring ever more powerful
selectors to override previous styling.

Avoid qualifying class names with type selectors. E.g. ``.widget`` is better
than ``div.widget``.

Avoid adjoining classes unless there's a good reason to do it.

Sometimes different elements share a class but have an additional modifier class
that extends the meaning and changes the styling. E.g. ``.message.error`` and
``.message.success``. You could simply take advantage of the cascade order and
declare the ``.error`` and ``.success`` classes after the ``.message`` class,
but you can't always ensure classes will be kept in the proper cascade order
(rules get moved around as style sheets are refactored, or they appear in
different style sheets imported at different points, etc). In those cases you
might prefer to create a single, more explicit modifier class rather than rely
on adjoined classes, e.g. ``.message-error`` and ``.message-success``.

However, don't try to CLASS ALL THE THINGS by creating a unique class for every
single element just for an easy style hook, or by creating oodles of generic
classes to apply fine-grained styling at the expense of requiring a string of
classes on each element in the markup.

**Bad:** ::

    /* Too specific */
    .module-news-title-main {
        font-family: 'League Gothic', sans-serif;
    }

    .module-news-title-sub {
        font-family: Georgia, serif;
    }

    /* Too generic (and presentational) */
    .size20 {
        font-size: 20px;
    }

    .size16 {
        font-size: 16px;
    }

It's usually better to style elements based on their context than to try to make
every possible style rule free-standing and every element 100% reusable in any
context on any page. Use descendant selectors judiciously but keep them simple.

**Good:** ::

    .module-news h2 {
        font: 20px 'League Gothic', sans-serif;
    }

    .module-news h3 {
        font: 16px Georgia, serif;
    }

Avoid ``!important`` in CSS unless absolutely necessary, **which it almost
never is**.

Some off-the-shelf frameworks/libraries/plugins include ``!important`` styles of
their own that you might have to override with another ``!important`` style, or
they write out inline styling into the DOM that you have to override in a style
sheet with ``!important``. (One could consider these transgressions to be
warning signs of a poorly made framework/library/plugin and you might want to
seek better options that don't force you to junk up your CSS.)

Fonts and typography
~~~~~~~~~~~~~~~~~~~~

It's alright to use pixels for ``font-size``.

For many years CSS authors eschewed pixels and favored relative units for font
sizing because IE 5 and 6 couldn't scale text set in absolute units (like ``px``).
All modern browsers can scale text in any unit (or zoom the entire page) so this
is no longer a driving concern, unless you're catering to versions of IE from
the previous century.

There are times when it's better to use relative ``font-size`` units like `em`s
or percentages. You may have a bit of text that should be sized proportionally
to a parent element whose font size is unknown. Some responsive designs call
for globally resizing text in different layouts (e.g. globally bigger text for
mobile), in which case it's simpler to change a single base size on a parent
than to re-declare the absolute ``font-size`` of each element.

Just remember that relative font sizes inherit and cascade so you can end up
with magic numbers like ``.6875em``. The ``rem`` unit (root em) can avoid the
cascade problems, but older browsers don't support rems and IE9 and 10 don't
support them in shorthand ``font`` declarations (fixed in IE11). It's always
something.

If you use ``rem``s for font sizing, include a ``px`` or other fallback
for older browsers.

Use `unit-less line-height`_. It doesn't inherit a percentage value of its
parent element, but instead is based on a multiplier of the font-size, whatever
that may be. E.g. ``line-height: 1.4;`` or in a shorthand ``font`` property:
``font: 14px/1.4 sans-serif;``. Don't use an absolute unit like ``px`` for
``line-height``; it creates more problems than it solves.

.. _unit-less line-height: https://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/

Use "`bulletproof font syntax`_" for webfonts. You usually don't need to include
SVG font files unless your project needs to target older versions of WebKit.
For modern browsers, TTF + WOFF is sufficient, as well as EOT for older
versions of IE (which may also be optional, depending on your target audience).
Example::

    @font-face {
        font-family: 'Open Sans';
        font-style: normal;
        font-weight: normal;
        src: url(/media/fonts/OpenSans-Bold-webfont.eot?#iefix) format('embedded-opentype'),
             url(/media/fonts/OpenSans-Bold-webfont.woff) format('woff'),
             url(/media/fonts/OpenSans-Bold-webfont.ttf) format('truetype');
    }


.. _bulletproof font syntax: https://blog.fontspring.com/2011/02/the-new-bulletproof-font-face-syntax/


Formatting CSS
--------------

When a rule has a group of selectors separated by commas, place each selector
on its own line.

The opening brace (``{``) of a rule's declaration block should be on the same
line as the selector (or the same line as the last selector in a group of
selectors).

Use a single space before the opening brace (``{``) in a rule, after the last
selector.

Put each declaration on its own line.

Indent the declaration block one level relative to its selector.

Use a colon (``:``) immediately after the property name, followed by a single
space, then the value.

Terminate each declaration with a semicolon (``;``), including the last
declaration in a block.

Put the closing brace (``}``) on its own line, aligned with the rule's selector.::

    .selector-1,
    .selector-2 {
        property: value;
        property: value;
    }

    .selector-3 {
        property: value;
    }

When you have a block of related rules, each with one or two declarations,
you can use a single-line format without any blank lines between rules. It
makes the block of related rules a bit easier to scan. In this case include
a single space after the opening brace and before the closing brace. Add
spaces after the selector to align the values.::

    .message-success { color: #080; }
    .message-error   { color: #ff0; }
    .message-notice  { color: #00f; }

Or::

    @keyframes bounce {
        0%   { bottom: 300px; }
        25%  { bottom: 30px; }
        50%  { bottom: 100px; }
        100% { bottom: 30px; }
    }

When possible, limit line lengths to 80 characters. This improves readability,
minimizes horizontal scrolling, makes it possible to view files side by side,
and produces more useful diffs with meaningful line numbers. There will be
exceptions such as long URLs or gradient syntax but most rules in CSS should
fit well within 80 characters even with indentation.

Long, comma-separated property values -- such as multiple background images,
gradients, transforms, transitions, webfonts, or text and box shadows -- can
be arranged across multiple lines (indented one level from their property).::

    .selector {
        background-image:
            linear-gradient(#fff, #ccc),
            linear-gradient(#f3c, #4ec);
        box-shadow:
            1px 1px 1px #000,
            2px 2px 1px 1px #ccc inset;
        transition:
            border-color .5s ease-in,
            opacity .1s ease-in;
    }

For vendor prefixed properties, use spaces to align the values, keeping the
property names left-aligned as usual::

    .selector {
        -webkit-box-shadow: 1px 2px 0 #ccc;
        -moz-box-shadow:    1px 2px 0 #ccc;
        -ms-box-shadow:     1px 2px 0 #ccc;
        -o-box-shadow:      1px 2px 0 #ccc;
        box-shadow:         1px 2px 0 #ccc;
    }

Or, when the value has the prefix::

    .selector {
        background: -webkit-linear-gradient(to bottom, #fff, #000);
        background:    -moz-linear-gradient(to bottom, #fff, #000);
        background:     -ms-linear-gradient(to bottom, #fff, #000);
        background:      -o-linear-gradient(to bottom, #fff, #000);
        background:         linear-gradient(to bottom, #fff, #000);
    }


Also notice this implies a specific order for vendor prefixes from longest to
shortest, mostly just for readability and consistency. It's convenient that the
unprefixed version, which always appears last, is shortest by default.


Whitespace
~~~~~~~~~~

Use spaces (or soft-tabs) with a four space indent. Never use tabs.

Eliminate trailing whitespace at the end of lines. Blank lines should have no
spaces.

Include one blank line between rules.

Include a single blank line at the end of files.


Property ordering
~~~~~~~~~~~~~~~~~

Order declarations alphabetically by property name (from A to Z), with a few
exceptions:

* Keep vendor prefixed properties together and ordered by length, with the
  unprefixed property last (see the earlier example).
* Keep positioning properties together, namely ``position``, ``top``, ``right``,
  ``bottom``, ``left``, and ``z-index``.
* You can optionally keep ``width`` and ``height`` together if you're declaring
  both.
* You can optionally keep some type-related properties together when that's
  sensible, such as ``font-size``, ``text-transform``, and ``letter-spacing``.

Many developers settle into their own system for ordering declarations based on
relevance, logical groupings, line length, or just semi-random as they're added.
Although alphabetical ordering can defy any other logical ordering -- adjacent
properties may have nothing in common while closely related properties can be
spread far apart -- at least there's no ambiguity about the alphabet and it's
easy to enforce the guideline across a team.

After all that, it's actually pretty rare for a single rule to hold so many
declarations that ordering becomes too much of a hassle. When in doubt,
alphabetize.


Naming conventions
------------------

Names should be semantically meaningful, descriptive of the element's content,
purpose, or function, not its presentation.

| **Bad:** ``.big-blue-button``, ``.right-column``, ``.small``
| **Good:** ``.button-submit``, ``.content-sub``, ``.field-note``

Many CSS frameworks, such as Twitter's Bootstrap and Zurb's Foundation, define
a lot of presentational classes for things like column widths, font sizes,
and button styles. If you're using such a framework, you can use those classes
as mixins in a preprocessed style sheet, rather than littering markup
with presentational names.

**Bad**::

    <div class="author-bio col-md-3 col-md-offset-2">

**Better**::

    .author-bio {
        .col-md-3;
        .col-md-offset-2;
    }

.. Note::

    For very large and complex sites, excessively repeating common declarations
    can lead to a lot of redundancy and CSS bloat. In those cases you can get
    better performance with some presentational classes if it leads to a
    significantly lighter style sheet. E.g. it can speed up a site considerably
    to specify column widths with a class in a few dozen HTML templates than to
    repeat the same width, float, and margin declarations a thousand times in
    CSS. We don't have many sites operating on the kind of scale that warrants
    that approach, but there are always exceptions.

Names should be as short as possible and as long as necessary.
Clarity is key. E.g. ``.prime-nav`` is better than ``.primary-navigation``,
but ``.article-author`` is better than ``.art-auth``.

Avoid overly abstract names that require a cheat sheet to understand.

| **Bad:** ``.color12``, ``.r2-c6``, ``.v``

Names should be all lower case, no camelcase.

| **Bad:** ``.badClassName``, **Better:** ``.betterclassname``

Separate words with hyphens, not underscores.

| **Bad:** ``.bad_class_name``, **Best:** ``.best-class-name``

Use US English spellings (sorry, rest of the world). CSS itself follows US
English so it's inconsistent to mix standard spellings like ``color: #000;``
with classes like ``.colour-picker``.


Style sheet organization
------------------------

It's hard to standardize on a particular structure for style sheets, especially
when it comes to preprocessors and other tools that import and concatenate
separate files. But that doesn't mean we can't try to stick to some basic
principles:

* Group related rules into sections.
* Give each section a title in a comment.
* Order rules in a section from general to specific (remember the cascade).
* Order sections in a style sheet from general to specific.
* Add three blank lines between the last rule in a section and the next
  section's title (clear separation between sections makes scanning easier).

A typical style sheet might be structured from top to bottom like so (only an
example):

1. A preamble comment with a table of contents and other info.
2. *Fonts* (webfonts need to be declared first so you can reference them further
   down the cascade).
3. *Reset* (global resets should be first so you can override them later).
4. *Base elements* (no IDs or classes here, just general elements like links,
   headings, lists, forms).
5. *Base layout* (setting up the general page layout for the entire site,
   arranging basic blocks like a global header, global footer, main content
   areas and sidebars).
6. *Global components/modules* (general purpose widgets that will be reused like
   button links, a sidebar menu, pagination, breadcrumbs, footnotes, a search
   form, error messages).
7. *Specific page layout* (pages that deviate from the base layout and need more
   more specific styling, like a home page, contact page, gallery page).
8. *Specific components/modules* (less generic, self-contained widgets that need
   more specific styling like a download button, a contact form, or a carousel).

Many (most) websites end up with a few one-off pages or subsets of pages that
require more specific styling, rules used only on those pages and nowhere else.
To avoid dumping everything into a single ever-expanding CSS file, it's usually
best practice to split it into separate style sheets and combine them
server-side so each page gets just the rules it needs.

For responsive layouts, collect all the rules for a given medium/viewport into a
single media query rather than repeat the same media query several times
throughout a style sheet.


Preprocessors
-------------

All of the above guidelines (those relating to formatting and organization, at
least) apply equally to vanilla CSS and to style sheets authored for a
preprocessor. Here are some additional guidelines specific to preprocessors:


Keep nesting simple
~~~~~~~~~~~~~~~~~~~

Nested rules in pre-processed CSS turn into descendant selectors in the
generated style sheet. The deeper the nesting, the more complex and specific the
selector will be. Don't nest rules unless necessary for context and specificity,
and don't nest rules just to group them together (use sectioning comments for
grouping).

All the declarations for the parent element should come before the nested rules.
Include a blank line before each nested rule to separate it from the rule or
declaration above it.

**Really Bad**::

    .wrapper {
        #sidebar {
            .modules {
                .module-news {
                    background: #ccc;
                    h2 {
                        font-size: 18px;
                    }
                    padding: 10px;
                }
            }
            width: 320px;
            float: right;
        }
    }

**Good**::

    .module-news {
        background: #ccc;
        padding: 10px;

        h2 {
            font-size: 18px;
        }
    }

Try to limit nesting to one or two levels. If you find yourself nesting rules
deeper than three levels, you probably need to reconsider your approach.

If you wouldn't need to use a descendent selector in vanilla CSS, you probably
don't need to nest it in a pre-processed style sheet.

::

    /* Unnecessary nesting; the nested class doesn't need the specificity */
    .module {
        background: #ccc;
        padding: 10px;

        .module-title {
            font-size: 18px;
        }
    }

    /* Two rules for two elements */
    .module {
        background: #ccc;
        padding: 10px;
    }

    .module-title {
        font-size: 18px;
    }

If the parent rule has no declarations, nesting isn't necessary at all. If you
need the specificity, use an ordinary descendant selector.

::

    /* Especially unnecessary nesting */
    .breadcrumbs {
        ul {
            li {
                display: inline;
                list-style: none;
            }
        }
    }

    /* Better */
    .breadcrumbs ul li {
        display: inline;
        list-style: none;
    }

    /* Best */
    .breadcrumbs li {
        display: inline;
        list-style: none;
    }


LESS vs. Stylus
~~~~~~~~~~~~~~~

Many current and past Mozilla websites use `LESS <http://lesscss.org/>`_ as a
CSS preprocessor. However, LESS appeared to be stagnating for a time and some
projects moved toward `Stylus <http://stylus-lang.com/>`_ as an
emerging contender under more active development (and also because Stylus has
some extra features and shares some traits with Python). LESS has since resumed
more active development, but in an effort to standardize across Mozilla webdev,
we're making the call: it's Stylus for us.

New Mozilla webdev projects should use Stylus for CSS preprocessing (or stick
with vanilla CSS). Sites currently using LESS should work toward converting to
Stylus as soon as practically feasible (`tools can help
<https://gist.github.com/cvan/5061790#file-less2stylus-js>`_). LESS isn't
forbidden, but prefer Stylus if you have a choice.


A Few Words About Stylus
~~~~~~~~~~~~~~~~~~~~~~~~

On the `Stylus website <http://stylus-lang.com/>`_, right at the top
of the home page, the creators crow a lot about how all these required CSS
syntax bits, like braces and colons and semicolons, are optional in Stylus, as
if they're a great annoyance that we've all been clamoring to abolish for years.

Well, Stylus still generates ordinary CSS in the end, and inserts all those
optional doodads on your behalf anyway because they're *still required in CSS*.
Just because Stylus makes them optional doesn't mean we should omit them,
especially if they make style sheets easier to read. For the sake of readability
and smoother collaboration, we should try to make CSS look like CSS.

Format your Stylus-flavored pre-processed files as if you were formatting
vanilla CSS. Do use mixins, variables, functions, etc. and take advantage of all
the flexible goodness Stylus offers, but it should still read like a CSS
document.

* Use CSS syntax (Stylus allows it).
* Include colons, semi-colons, and braces.
* Identify variables with a dollar sign (``$``). It's optional in Stylus
  but makes variables easier to spot by humans.


**Bad** (though valid in Stylus)::

    .module
        background light-background
        h2
            font-size h-medium


**Good** (and still valid in Stylus)::

    .module {
        background: $light-background;
        h2 {
            font-size: $h-medium;
        }
    }


A Note on Sass/SCSS/Compass
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Very few (if any?) Mozilla projects use `Sass <https://sass-lang.com>`_ because
it requires Ruby. While Sass is a fine tool, and can be awesome in combination
with Compass, adding Ruby to our dev stack is a bridge too far. Sorry Rubyists;
we're a Python shop.

Even so, all the same formatting and organizational guidelines can apply just
as well to Sass/SCSS. Live long and prosper.


Validate!
---------

Validate your CSS with the `W3C's online tool <https://github.com/w3c/css-validator>`_
or equivalent.

Validation tools may report errors or give warnings for vendor prefixes, as they
should. It's something to be mindful of but it's perfectly fine to use prefixed
properties if you're doing it right.

Validation *warnings* are very different from validation *errors*. You should
take warnings under consideration and address them if needed, but errors are
real problems that you need to fix.

If you're using a preprocessor you'll obviously only be able to validate the
generated plain CSS, which can make it harder to track down where the errors
appear in the source files. A well organized style sheet can ease the pain.


A Note on CSS Lint
~~~~~~~~~~~~~~~~~~

`CSS Lint <http://csslint.net/>`_ is a useful tool and we recommend it, but take
its results with a grain of salt. Many of Lint's rules are phrased like
absolute edicts when they're more like soft warnings of things to be mindful of
(e.g. "Don't use too many floats"). Lint also forbids some things we expressly
allow in our own guidelines (e.g. "Don't use ID selectors"). If your file gets a
slew of warnings from CSS Lint that doesn't mean it's bad, just be able to
justify your decisions.

`This shortcut to CSS Lint`_ disables some of the more stringent rules we don't
necessarily abide.

.. _This shortcut to CSS Lint: http://csslint.net/#warnings=display-property-grouping,duplicate-properties,empty-rules,known-properties,adjoining-classes,compatible-vendor-prefixes,vendor-prefix,fallback-colors,star-property-hack,underscore-property-hack,bulletproof-font-face,font-faces,universal-selector,unqualified-attributes,zero-units,overqualified-elements,shorthand,floats,important,outline-none


FAQ
---

**Q:** [insert question]

**A:** It depends.
