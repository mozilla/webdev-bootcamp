Data storage and retrieval
==========================

Most sites have fairly simple data-layers.  The notable exception is Socorro.

Typically we use some form of mysql with master-slave replication.

For search either Sphinx or Elastic Search are used.

For cache memcache and redis.

Socorro uses postgres and HBase.

Production Data
---------------

Sometimes having production-like data is necessary for debugging.
Private data relating to users *must* remain on the Mozilla network.
Therefore,
there are two options for
getting Production or production-like MySQL data.

Anonymous Data
~~~~~~~~~~~~~~

In `~ddash/anonymize` On `cm-webdev01-master01` on the Mozilla/MPT VPN are
anonymized dumps of production data for:

    * AMO
    * FlightDeck
    * SUMO

While the datasets are anonymous, they are not for general distribution.


Input Data
~~~~~~~~~~

.. highlight:: bash

You can get a copy of the
Firefox Input database by using the following script::

        set -e
        FILE=input_mozilla_com.`date +%Y.%m.%d`.sql.gz
        USERNAME=username
        LOCAL_DB=firefox_input

        scp $USERNAME@cm-webdev01-master01:~ddash/input_mozilla_com/$FILE .
        zgrep -v "INSERT INTO \`feedback_term\`" $FILE > tmp.sql
        cat tmp.sql |mysql -u root $LOCAL_DB
        rm tmp.sql $FILE

Be sure to replace ``username`` with your actual LDAP username.


.. _db-cluster:

Webdev Database Cluster
~~~~~~~~~~~~~~~~~~~~~~~
Alternately, many production databases have copies running on
`cm-webdev01-master01` and `cm-webdev01-slave01`.  You can connect directly to
these servers.
