Testing
=======

Testing is a very important part of the development process. It allows us to
verify the functionality of our projects as well as judge the quality of our
work.

At Mozilla, we have multiple ways of testing our code, including:

- Unit tests and integration tests, which are automated tests that verify that
  pieces of code work as expected.
- End-to-end tests, automated tests which check the functionality of a project
  as a whole. For example, simulating clicks in a web browser to test how a
  site functions.
- Manual testing, which is performed by a human and involves verifying features
  work as expected and exploratory tests.

Assessing and managing risk
---------------------------

The end goal of testing is to manage the risk of something going wrong with
your project. To this end, one of the first steps you should take is to assess
the risk of each area of your project.

More concretely, some parts of your project are going to be more likely to fail
than others. Also, some parts of your project are more important than others,
and it may be more harmful for them to fail than less important parts.

A risk assessment lists out the different parts of your project (such as
certain web pages or parts of an API) and ranks them based on their importance.
For example, a news site would rank being able to read existing articles as more
important than being able to submit new articles. This kind of ranking allows
you to make better decisions about which parts of your project to test more and
what kind of tests to run.

Unit and integration tests
--------------------------

As a developer, the most common type of tests you will write are unit tests and
integration tests. Unit tests test the smallest possible chunk of functionality
and are isolated from each other, whereas integration tests test the interaction
between these chunks.

In practice, **any changes you make to a project should be tested in some
automated way if it's reasonable to do so.** While each project varies,
generally Webdev isn't picky about having perfect unit tests or perfect test
isolation. If you're unsure, look at the project's existing tests for
guidance on the preferred style.

Mozilla uses `TaskCluster`_ to run these tests automatically for continuous
integration. Other projects rely on `Travis CI`_ for executing their tests.

For Django projects, these tests live within the ``tests`` module of each
included Django application. For Node-based projects, they normally live in
a directory named ``test`` or ``tests`` at the root of the repository. Refer to
your project's documentation for more details.

.. _TaskCluster: https://docs.taskcluster.net/

End-to-end tests
----------------

End-to-end tests simulate how your project will be used by end users and verify
that it behaves as expected. This is most commonly applied to websites, where
we use tools like `Selenium`_ to simulate users interacting with the website.

For many sites, these tests are written by `Web QA`_ contributors and run
against the various :doc:`server environments <servers>`.

.. _Selenium: https://wiki.mozilla.org/Websites/Domain_List
.. _Web QA: https://blog.mozilla.org/webqa/

Manual testing
--------------

Manual testing is good old-fashioned human-powered testing, where a living,
breathing human uses your project and checks for any errors. Typically this is
either for verifying that a new feature works as expected, or for free-form
exploratory testing.

In addition to writing automated tests, you almost certainly should be manually
testing any changes you make to a project.

Testing tools
-------------

The following is a non-exhaustive, possibly-out-of-date list of tools and
libraries that may aid you in testing your projects.

General
^^^^^^^

- Jenkins_ is a continuous integration server that builds and/or tests software
  projects continuously.
- `Travis CI`_ is a hosted continuous integration service that integrates with
  GitHub.
- Selenium_ is a tool for automating browsers, often for testing purposes.

.. _Jenkins: https://jenkins.io/
.. _Travis CI: https://travis-ci.org/

Python
^^^^^^

- nose_ is a highly recommended testing library for Python.

   - `django-nose`_ integrates nose into a Django test runner.
   - `nose-progressive`_ is a nose plugin that makes test output much easier
     to read.

- `factory_boy`_ replaces test fixtures with factories that generate test
  objects easily. It integrates with the `Django ORM`_ to generate model instances
  with a very convenient syntax.

- Mock_ is one of the most popular libraries for replacing parts of the system
  you're testing with mock objects and asserting things about their behavior.

.. _nose: https://nose.readthedocs.io/
.. _django-nose: https://github.com/django-nose/django-nose
.. _nose-progressive: https://github.com/erikrose/nose-progressive
.. _factory_boy: https://factoryboy.readthedocs.io/
.. _Mock: http://www.voidspace.org.uk/python/mock/
.. _Django ORM: https://docs.djangoproject.com/en/2.0/topics/db/

Node / JavaScript
^^^^^^^^^^^^^^^^^

- Mocha_ is a framework for running tests on Node.js and in the browser.
- Chai_ is an assertion library with many interfaces to accommodate different
  testing styles.
- Karma_ allows you to execute JavaScript code in multiple real browsers.

.. _Mocha: https://mochajs.org/
.. _Chai: http://chaijs.com/
.. _Karma: https://karma-runner.github.io
