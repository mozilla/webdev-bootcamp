Server Environments
===================

Writing code is one thing, but getting it live on a public server is another.
This document explains some high-level details of our server environments and
how we deploy our websites.

Development, staging, and production
------------------------------------

Most Mozilla websites are split into three environments:

- Development (AKA Dev) usually runs off of the latest code that has been
  committed for a project by updating regularly throughout the day. Dev is
  useful for testing new features and getting feedback.

  The standard pattern for dev server URLs is ``project-dev.allizom.org``.

- Staging (AKA stage) is intended to be similar to production and is used for
  testing the deployment process itself. Stage is usually deployed before
  deploying to production, and is sometimes used by QA for testing purposes as
  well.

  The standard pattern for stage server URLs is ``project.allizom.org``.

- Production (AKA prod) is the live instance of the site. It is the environment
  that users see when they visit your site. Admin interfaces and other
  sensitive areas of a site are generally locked down in this environment.

  The standard pattern for production server URLs is ``project.mozilla.org``.
