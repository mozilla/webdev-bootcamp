Error handling in production
============================

When a traceback occurs in production sites, you need to send it somewhere.
Normally Django sends emails which can work fine until you get a few
thousand error emails in a minute.

Optionally, you can use `Arecibo`_ to track your errors. There are currently
three servers, all requiring Mozilla LDAP access:

* http://amckay-arecibo.khan.mozilla.org/ test server, play around here.
* https://arecibo-sjc.mozilla.org/ one in the SJC data centre. To post to this
  instance use the following URL in your Django config: http://arecibo1.dmz.sjc1.mozilla.com/
* https://arecibo-phx.mozilla.org/ one in the PHX data centre *preferred*. To
  post to this instance, use the following URL in your Django config: http://arecibo1.dmz.phx1.mozilla.com/

The PHX data centre server is on a dedicated box, where as SJC is in a VM. Please
use the PHX one if possible.

To send errors from playdoh, see the `playdoh`_ docs.

.. _playdoh: http://readthedocs.org/docs/playdoh/en/latest/errors.html
.. _Arecibo: http://areciboapp.com
