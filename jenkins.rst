.. index:: ci;jenkins

.. _ci-chapter:

===============================
Jenkins: Continuous Integration
===============================


We have a public instance of Jenkins_ (formerly Hudson). For most
projects it runs their python test suite. Optionally we use it to do
JS testing as well as any menial tasks that need to be done regularly,
like packaging. If you break things you will be warned in IRC.

.. _jenkins: https://jenkins.mozilla.org/

Adding a new Project
--------------------

If you've got tests (which you should), and you are deploying to production,
you might want to add your project to Jenkins_.  This let's the world know just
how wonderful you are at writing tests.

To do this you'll need to:

1. Log in via LDAP to Jenkins_.
2. Start a new project.
3. Copy Affiliates.
4. Update the notification settings (IRC, email, etc).
5. Copy the ``bin/jenkins.sh`` script from playdoh if you don't have it.
6. Make sure it's got ``+x`` permissions.

You may need to make some adjustments according to the needs of your particular
project.
