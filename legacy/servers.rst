.. index:: servers

Servers
=======

We have a number of servers that you'll regularly encounter as a web dev.

**khan** is a development server. If you choose not to develop locally, this
option is available.

**\*.allizom.org**: all our staging servers share this domain.

**webdev1.db.scl3.mozilla.com** is the webdev mysql server. See
:ref:`db-cluster`.

**cm-vpn01** is where our server logs are copied. Note that you need to file a
bug to get access to this server.

Served Environments
-------------------

There are two or three main environments for our web sites:

* **dev** (currently "stage" or "preview") which serves the latest `master`.
* **stage**

  * Currently ``amo-next`` and ``crash-stats.stage`` are our only "stage"
    environments.
  * This is what will go live to production.

* **production**

.. _vpn-info:

VPN
---

To get to any Mozilla servers you will need VPN access. There are two VPN
networks: Mozilla-MV_ (Mountain View office VPN) and Mozilla-VPN_ (also known
as the Datacenter VPN).

If you want to use Mozilla's shared network volumes (like ``fs2``) you can
connect to the Mozilla-MV VPN.

You'll need to connect to the Mozilla VPN if you want to access anything in the
data centres (such as khan, any database server, etc). All Mozilla employees with
a valid LDAP login have access to this VPN by default.

On OS X, we recommend Viscosity_ for VPN.

.. _Mozilla-MV: https://intranet.mozilla.org/JumpHost
.. _Mozilla-VPN: https://mana.mozilla.org/wiki/pages/viewpage.action?pageId=30769829
.. _Viscosity: https://intranet.mozilla.org/IT_MPT-RemoteAccess#Viscosity_.28TunnelBlick_alternative.29
