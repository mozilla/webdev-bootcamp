Servers
=======

We have a number of servers that you'll regularly encounter as a web dev.

**khan** is a development server.  If you choose not to develop locally, this
option is available.

**\*.allizom.org**: all our staging servers share this domain.

**cm-webdev01-master01** is the webdev mysql server.  See :ref:`db-cluster`.

**cm-vpn01** is where our server logs are copied.

Served Environments
-------------------

There are two or three main environments for our web sites:

* **dev** (currently "stage" or "preview") which serves the latest `master`.
* **stage**
  * (currently ``amo-next`` and ``crash-stats.stage``) are our only
    "stage" environments.
  * This is what will go live to production.
* **production**

VPN
---

To get to any Mozilla servers you will need VPN access.

We recommend Viscosity_ for VPN.

.. _Viscosity: https://intranet.mozilla.org/IT_MPT-RemoteAccess#Viscosity_.28TunnelBlick_alternative.29
