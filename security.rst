Security
========

As you are reading this guide, it can be assumed that you will be building web
applications for Mozilla. While there is a web security team, building secure
services is your responsibility, too. This guide will give you a quick heads-up
on important topics.

.. security team, etc.?


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

`CSP 1.1`_ is already being drafted at the w3c, but you should focus on CSP 1.0
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
    will gladly help (``fbraun``).

So, how is CSP able to mitigate XSS and similar attacks? Your whitelist enables
you to only include origins you trust. It might prove difficult and much more
risky for an attacker to compromise one of the trusted hosts. However, there is
a caveat to the protection of CSP. Since the origin of inline code cannot be
decided upon by the browser (was it intended or attacker-injected?), it is
blocked by default. Furthermore, since eval-like constructs pose a security risk
if an attacker is able to inject code, they are disabled by default, too.

There may be occasions, where such CSP-incompatible code is unavoidable. but in
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

* Inline script elements have to be combined to externalized scripts and loaded
  via ``<script src="URL"></script>``. In consequence, you trade some
  performance for additional security.
* Inline event handlers can be completely avoided with two strategies: First,
  you can attach event handlers via external scripts, using the addEventListener
  API of JavaScript. Additionally, you can let even bubbling work for you (e.g.
  JQuery's ``$.live``).
* The JS pseudo protocol can be entirely avoided with attached click event
  handlers.
* Code in inline style elements can be externalized to CSS files and loaded via
  ``<link>``.
* Avoiding inline style attributes can be achieved with a clean structure of the
  document and potentially adding classes/IDs to your markup. This should give
  you plenty of options to select the corresponding nodes from an external
  stylesheet.
* If your code sets style attributes with JavaScript, you might want to consider
  using APIs like ``node.style``.
* Double-check all your eval-using code. Does it really need eval? If it does,
  you generally can't avoid whitelisting 'unsafe-eval'.


Projects simplifying the use of CSP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Python/Django: https://github.com/mozilla/django-csp
* Node.js/Express: https://github.com/evilpacket/helmet


.. _`all major browsers`: http://caniuse.com/#search=content%20security%20policy
.. _`Content Security Policy`: http://www.w3.org/TR/CSP/
.. _`CSP 1.1`: https://dvcs.w3.org/hg/content-security-policy/raw-file/tip/csp-specification.dev.html
.. _`MDN pages`: https://developer.mozilla.org/en/docs/Security/CSP
