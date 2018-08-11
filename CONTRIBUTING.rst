.. highlight:: shell

============
Contributing
============

Contributions are welcome, and they are greatly appreciated! Every little bit
helps, and credit will always be given.

You can contribute in many ways:

Types of Contributions
----------------------

Report Bugs
~~~~~~~~~~~

Report bugs at https://github.com/HDI-Project/MLPrimitives/issues.

If you are reporting a bug, please include:

* Your operating system name and version.
* Any details about your local setup that might be helpful in troubleshooting.
* Detailed steps to reproduce the bug.

Fix Bugs
~~~~~~~~

Look through the GitHub issues for bugs. Anything tagged with "bug" and "help
wanted" is open to whoever wants to implement it.

Implement Features
~~~~~~~~~~~~~~~~~~

Look through the GitHub issues for features. Anything tagged with "enhancement"
and "help wanted" is open to whoever wants to implement it.

Write Documentation
~~~~~~~~~~~~~~~~~~~

MLPrimitives could always use more documentation, whether as part of the
official MLPrimitives docs, in docstrings, or even on the web in blog posts,
articles, and such.

Submit Feedback
~~~~~~~~~~~~~~~

The best way to send feedback is to file an issue at https://github.com/HDI-Project/MLPrimitives/issues.

If you are proposing a feature:

* Explain in detail how it would work.
* Keep the scope as narrow as possible, to make it easier to implement.
* Remember that this is a volunteer-driven project, and that contributions
  are welcome :)

Get Started!
------------

Ready to contribute? Here's how to set up `MLPrimitives` for local development.

1. Fork the `MLPrimitives` repo on GitHub.
2. Clone your fork locally::

    $ git clone git@github.com:your_name_here/MLPrimitives.git

3. Install your local copy into a virtualenv. Assuming you have virtualenvwrapper installed,
   this is how you set up your fork for local development::

    $ mkvirtualenv MLPrimitives
    $ cd MLPrimitives/
    $ pip install -e .
    $ pip install -r requirements_dev.txt

4. Create a branch for local development::

    $ git checkout -b name-of-your-bugfix-or-feature

   Now you can make your changes locally.

5. While hacking your changes, make sure to cover all your developments with the required
   unit tests, and that none of the old tests fail as a consequence of your changes.
   For this, make sure to run the tests suite and check the code coverage::

    $ make test       # Run the tests
    $ make coverage   # Get the coverage report

6. When you're done making changes, check that your changes pass flake8 and the
   tests, including testing other Python versions with tox::

    $ make test-all

7. Make also sure to include the necessary documentation in the code as docstrings following
   the [google](https://google.github.io/styleguide/pyguide.html?showone=Comments#Comments)
   or the [numpy](https://numpydoc.readthedocs.io/en/latest/format.html) docstring style.
   If you want to view how your documentation will look like when it is published, you can
   generate and view the docs with this command::

    $ make viewdocs

8. Commit your changes and push your branch to GitHub::

    $ git add .
    $ git commit -m "Your detailed description of your changes."
    $ git push origin name-of-your-bugfix-or-feature

9. Submit a pull request through the GitHub website.

Pull Request Guidelines
-----------------------

Before you submit a pull request, check that it meets these guidelines:

1. It resolves an open GitHub Issue and contains its reference in the title or
   the comment. If there is no associated issue, feel free to create one.
2. Whenever possible, it resolves only **one** issue. If your PR resolves more than
   one issue, try to split it in more than one pull request.
3. The pull request should include unit tests that cover all the changed code
4. If the pull request adds functionality, the docs should be updated. Put
   your new functionality into a function with a docstring, and add the
   feature to the list in README.rst.
5. The pull request should work for Python2.7, 3.4, 3.5 and 3.6. Check
   https://travis-ci.org/HDI-Project/MLPrimitives/pull_requests
   and make sure that all the checks pass.

Unit Testing Guidelines
-----------------------

All the Unit Tests should comply with the following requirements:

1. Unit Tests should be based only in unittest and pytest modules.

2. The tests that cover a module called ``mlprimitives/path/to/a_module.py`` should be
   implemented in a separated module called ``tests/mlprimitives/path/to/test_a_module.py``.
   Note that the module name has the ``test_`` prefix and is located in a path similar
   to the one of the tested module, just inside te ``tests`` folder.

3. Each method of the tested module should have at least one associated test method, and
   each test method should cover only **one** use case or scenario.

4. Test case methods should start with the ``test_`` prefix and have descriptive names
   that indicate which scenario they cover.
   Names such as ``test_some_methed_input_none``, ``test_some_method_value_error`` or
   ``test_some_method_timeout`` are right, but names like ``test_some_method_1``,
   ``some_method`` or ``test_error`` are not.

5. Each test should validate only what the code of the method being tested does, and not
   cover the behavior of any third party package or tool being used, which is assumed to
   work properly as far as it is being passed the right values.

6. Any third party tool that may have any kind of random behavior, such as some Machine
   Learning models, databases or Web APIs, will be mocked using the ``mock`` library, and
   the only thing that will be tested is that our code passes the right values to them.

7. Unit tests should not use anything from outside the test and the code being tested. This
   includes not reading or writting to any filesystem or database, which will be properly
   mocked.

Tips
----

To run a subset of tests::

    $ pytest tests.test_mlprimitives

Release Workflow
----------------

The process of releasing a new version involves several steps combining both ``git`` and
``bumpversion`` which, briefly:

1. Merge what is in ``master`` branch into ``stable`` branch.
2. Update the version in ``setup.cfg``, ``mlprimitives/__init__.py`` and ``HISTORY.md`` files.
3. Create a new TAG pointing at the correspoding commit in ``stable`` branch.
4. Merge the new commit from ``stable`` into ``master``.
5. Update the version in ``setup.cfg`` and ``mlprimitives/__init__.py`` to open the next
   development interation.

**Note:** Before starting the process, make sure that ``HISTORY.md`` has a section titled
**Unreleased** with the list of changes that will be included in the new version, and that
these changes are committed and available in ``master`` branch.
Normally this is just a list of the Pull Requests that have been merged since the latest version.

Once this is done, just run the following commands::

    git checkout stable
    git merge --no-ff master    # This creates a merge commit
    bumpversion release   # This creates a new commit and a TAG
    git push --tags origin stable
    make release
    git checkout master
    git merge stable
    bumpversion --no-tag patch
    git push