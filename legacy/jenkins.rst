.. index:: ci;jenkins

.. _ci-chapter:

===============================
Jenkins: Continuous Integration
===============================


We have a public instance of Jenkins_ (formerly Hudson). For most projects it
runs their python test suite. Optionally we use it to do JS testing as well as
any menial tasks that need to be done regularly, like packaging. If you break
things you will be warned in IRC.

.. _jenkins: https://ci.mozilla.org/

Adding a new Project
--------------------

If you've got tests (which you should), and you are deploying to production, you
might want to add your project to Jenkins_. This let's the world know just how
wonderful you are at writing tests.

Asumming you're working on ``mozilla/awesome_project``, you'll need to:

- On Jenkins:

  1. Log in via LDAP to Jenkins_.
  2. Start a new project.
  3. Copy Affiliates.
  4. Update the notification settings (IRC, email, etc).
  5. Update the Github project to point to ``https://github.com/mozilla/awesome_project/``
  6. Update the Git repository to point to ``git://github.com/mozilla/awesome_project.git``
  7. Check the "Build when a change is pushed to GitHub" checkbox

- In your repo:

  1. Copy the ``bin/jenkins.sh`` script from playdoh if you don't have it.
  2. Make sure it's got ``+x`` permissions.

- On Github:

  1. Go to ``https://github.com/mozilla/awesome_project/admin/hooks``
  2. The hook URL is ``https://ci.mozilla.org/github-webhook/``

You may need to make some adjustments according to the needs of your particular
project.

Interacting with Jenkins on IRC
-------------------------------

You can get a Jenkins bot in your channel to send him commands.

1. Go to the general configuration https://ci.mozilla.org/configure
2. Add your channel in the IRC Notification section

You can now run commands such as ``jenkins: build awesome_project now``
