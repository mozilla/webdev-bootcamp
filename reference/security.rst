Security
========

This guide will give you a quick heads-up on important security topics to keep
in mind as you work on your projects.


Involving the Security Team
---------------------------

The security teams can be easily involved by setting the ``sec-review`` flag to
``?`` in Bugzilla. It is highly encouraged to do that early in the development
process. For bigger projects the `Security Review Process`_ should be taken into
account, so that security considerations are resolved before the day of
deployment dawns. If you have small questions, feel free to flag someone for
``feedback`` or ask in #security on IRC.


X-Frame-Options
---------------

X-Frame-Options (XFO) is a security header (i.e. in your HTTP response) that
states whether your site should be framed or not. For several reasons laid out
in this `blog post`_, you should default to **DENY**.

If you do need to be framed, you can restrict this to web pages in the same
origin (people sometimes think "same domain", but it's actually the protocol,
domain name and port forming the security scope of a website).
There are detailed docs about `XFO on MDN`_ and there are additional resources
that show you how to set up X-Frame-Options in your `Django`_ and `NodeJS`_
projects.


Content Security Policy
-----------------------

.. note::
    When building web applications, it is best to incorporate
    Content Security Policy (CSP) early into the development process. You may
    find it substantially harder to apply CSP to existing projects because of
    the way it restrains the capabilities of your code.

`Content Security Policy`_ (CSP) is a security header which is able to mitigate
some client-side attacks on web applications, like Cross-Site Scripting (XSS).
Think of CSP as a whitelist of resources which are allowed to be embedded into
your HTML documents. As CSP does not prevent flaws from being exploited but merely
mitigates the effects, you should never solely rely on it. `CSP 1.1`_ is already
being drafted at the W3C, but you should focus on CSP 1.0 - mainly because of
its `wide adoption among browsers`_. Head on over to `MDN`_ for more information
on this topic.


CSP usage
~~~~~~~~~

.. warning::
    ``*`` wildcards pose a security risk and should be completely avoided in
    critical directives like ``style-src``, ``object-src`` and ``script-src``.
    If you are unsure about a certain case, members of the web security team
    will gladly help (See `Involving the Security Team`_).

To avoid CSP problems, follow these guidelines:

* Don't use inline JavaScript code. This includes inline script elements
  (``<script>code</script>``), inline event handlers (e.g.
  ``<button onclick="code">Click me</button>``) and the JavaScript pseudo
  protocol (``<a href="javascript:code">Click me</a>``).
* Don't use inline CSS code. This includes inline style elements
  (``<style>code</style>``) and inline style attributes
  (``<button style="code"></button>``).
* Don't use ``eval``, ``setTimeout('string', time)``,
  ``setInterval('string', time)``, ``Function('string')()`` or any other
  eval-like construct.

Here are some strategies for avoiding common CSP errors:

:Inline script elements:
    Should go into a JS file.
:Inline event handlers:
    Attach event handler in an external JS file (addEventListener) or let event
    bubbling work for you (e.g. JQuery's $.live).
:JS pseudo protocol:
    Attach click event handler to the node (see above)
:Inline style elements:
    These can be easily put into an external CSS file
:Inline style attributes:
    Add classes or IDs to your markup and handle those in an external CSS file
:Inline style attributes which are set via JavaScript:
    Use the ``element.style`` property instead of ``element.setAttribute``.


Projects simplifying the use of CSP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Python/Django: https://github.com/mozilla/django-csp
* Node.js/Express: https://github.com/evilpacket/helmet


.. _`wide adoption among browsers`: https://caniuse.com/#search=content%20security%20policy
.. _`Content Security Policy`: https://www.w3.org/TR/CSP/
.. _`CSP 1.1`: https://dvcs.w3.org/hg/content-security-policy/raw-file/tip/csp-specification.dev.html
.. _`MDN`: https://developer.mozilla.org/docs/Security/CSP
.. _`Security Review Process`: https://wiki.mozilla.org/Security/ReviewProcess
.. _`blog post`: https://blog.mozilla.org/security/2013/12/12/on-the-x-frame-options-security-header/
.. _`XFO on MDN`: https://developer.mozilla.org/docs/HTTP/X-Frame-Options
.. _`Django`: https://docs.djangoproject.com/en/dev/ref/clickjacking/
.. _`NodeJS`: https://npmjs.org/package/helmet
