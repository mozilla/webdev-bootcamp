Security
========

As you are reading this guide, it can be assumed that you will be building web
applications for Mozilla. While there is a web security team, building secure
services is your responsibility, too. This guide will give you a quick heads-up
on important topics.

Involving the Security Team
---------------------------

The security teams can be easily involved by setting the ``sec-review`` flag
to ``?`` in Bugzilla. It is highly encouraged to do that early in the developement
process. For bigger projects the `Security Review Process`_ should be taken
into account, so that security considerations are resolved before the day of
deployment dawns. If you have small questions, feel free to flag someone for ``feedback`` or ask in #security on IRC.


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

`Content Security Policy`_ (CSP) is a mechanism, which is able to mitigate some
client-side attacks on web applications, like Cross-Site Scripting (XSS). Except
from Internet Explorer, it is implemented in `all major browsers`_. As CSP does
not prevent flaws from being exploited but merely mitigates the effects, you
should never solely rely on it. However, CSP can be seen as another security
layer on top of your other defenses (this concept is called defense in depth).
In consequence, adversaries have to overcome multiple hurdles until they can do
harm, increasing the cost of the attack.

`CSP 1.1`_ is already being drafted at the W3C, but you should focus on CSP 1.0
- mainly because of its wide adoption among browsers. There are multiple
`MDN pages`_ giving greater detail on some of the topics of the following
paragraphs.

Think of CSP as a whitelist of resources which are allowed to be embedded into
your HTML documents. Resources are categorized into directives, each controlling
a different type. There are 9 resource-controlling directives: ``default-src``,
``script-src``, ``object-src``, ``style-src``, ``img-src``, ``media-src``,
``frame-src``, ``font-src`` and ``connect-src``. Any of these directives take a
space separated list of so-called sources. Head on over to MDN to see some
examples.

.. warning::
    ``*`` wildcards pose a security risk and should be completely avoided in
    critical directives like ``style-src``, ``object-src`` and ``script-src``.
    If you are unsure about a certain case, members of the web security team
    will gladly help (See `Involving the Security Team`_).

So, how is CSP able to mitigate XSS and similar attacks? Your whitelist enables
you to only include origins you trust. It might prove difficult and much more
risky for an attacker to compromise one of the trusted hosts. However, there is
a caveat to the protection of CSP. Since the origin of inline code cannot be
decided upon by the browser (was it intended or attacker-injected?), it is
blocked by default. Furthermore, since eval-like constructs pose a security risk
if an attacker is able to inject code, they are disabled by default, too.

There may be occasions, where such CSP-incompatible code looks unavoidable. but in
general you should always strive to follow these guidelines:

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

Here are some general strategies to avoid such code:

:Inline script elements:
    Should go into a JS file.
:Inline event handlers:
    Attach event handler through a DOMContentLoaded event in an external JS file
    (addEventListener) or let event bubbling work for you (e.g. JQuery's $.live).
:JS pseudo protocol:
    Attach click event handler to the node (see above)
:Inline style elements:
    These can be easily put into an external CSS file
:Inline style attributes:
    Add classes or IDs to your markup and handle those in an external CSS file
:Inline style attributes which are set via JavaScript:
    Use the ``elmt.style`` attribute instead of ``elmt.setAttribute``.


.. _`all major browsers`: http://caniuse.com/#search=content%20security%20policy
.. _`Content Security Policy`: http://www.w3.org/TR/CSP/
.. _`CSP 1.1`: https://dvcs.w3.org/hg/content-security-policy/raw-file/tip/csp-specification.dev.html
.. _`MDN pages`: https://developer.mozilla.org/en/docs/Security/CSP
.. _`Security Review Process`: https://wiki.mozilla.org/Security/ReviewProcess
.. _`blog post`: https://blog.mozilla.org/security/2013/12/12/on-the-x-frame-options-security-header/
.. _`XFO on MDN`: https://developer.mozilla.org/en-US/docs/HTTP/X-Frame-Options
.. _`Django`: https://docs.djangoproject.com/en/dev/ref/clickjacking/#
.. _`NodeJS`: https://npmjs.org/package/helmet
