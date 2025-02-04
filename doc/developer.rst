
*********
Developer
*********

This section details common practices and tips for contributors
to SmartSim and SmartRedis

================
Testing SmartSim
================

.. note::

    This section describes how to run the SmartSim (infrastructure library)
    test suite. For testing SmartRedis, see below

SmartSim utilizes ``Pytest`` for running its test suite. In the
top level of SmartSim, users can run multiple testing commands
with the developer Makefile

.. code-block:: text

    Test
    -------
    test                       - Build and run all tests
    test-verbose               - Build and run all tests [verbosely]
    test-cov                   - run python tests with coverage

.. note::

  For the test to run, you must have the ``requirements-dev.txt``
  dependencies installed in your python environment.


Local
=====

There are two levels of testing in SmartSim. The first
runs by default and doesn't launch any jobs out onto
a system through a workload manager like Cobalt.

If any of the above commands are used, the test suite will
run the the "light" test suite by default


PBSPro, Slurm, Cobalt
=====================

To run the full test suite, users will have to be on a system
with one of the above workload managers. Additionally users will
need to obtain an allocation of at least 3 nodes.

.. code-block:: bash

  # for slurm (with srun)
  salloc -N 3 -A account --exclusive -t 00:10:00

  # For PBSPro (with aprun)
  qsub -l select=3 -l place=scatter -l walltime=00:10:00 -q queue

  # for Cobalt (with aprun)
  qsub -n 3 -t 00:10:00 -A account -q queue -I

Values for queue and account should be substituted appropriately.

Once in an interative allocation, users will need to set the test
launcher environment variable: ``SMARTSIM_TEST_LAUNCHER`` to one
of the following values

 - slurm
 - cobalt
 - pbs
 - local

-------------------------------------------------------

==================
Testing SmartRedis
==================

.. include:: ../smartredis/doc/testing.rst
   :start-line: 3

-------------------------------------------------------

============
Git Workflow
============

Setup
=====

  - Fork the SmartSim (SmartRedis) repository
  - Set upstream as the main repository and set upstream push remote to ``no_push``
  - Follow installation instructions


Pull Requests
=============

Please check the following before submitting a pull request to the SmartSim repository

  1) Your feature is on a new branch off master.
  2) You are merging the feature branch from your fork into the main repository.
  3) All unnecessary whitespace has been purged from your code.
  4) Black and isort have been applied to format code and sort imports
  5) Pylint errors have been minimized as much as possible
  6) All your code as been appropriately documented.
  7) The PR description is clear and concise.
  8) You have requested a review.

Merging
=======

When merging there are a few guidelines to follow

   - Wrap all merge messages to 70 characters per line.


-------------------------------------------------------


=================
Python Guidelines
=================

For the most part, the conventions are to follow PEP8 that is supplied by pylint. However, there
are a few things to specifically mention.

  - Underscores should precede methods not meant to be used outside a class
  - All methods should have docstrings (with some exceptions)
  - Variable names should accurately capture what values it is storing without being overly verbose
  - No bad words
  - Use Black and isort frequently
  - Utilize ``conftest.py`` for creating pytest fixtures


---------------------------------------------------------

==================
Editor Suggestions
==================

The editor that we suggest developers to use is VSCode. Below are some extensions that
could make the process of developing on SmartSim a bit easier.

    - GitLens, for viewing changes in the git history
    - Remote SSH, for connecting to clusters and supercomputers
    - PyLance, Langauge Server
    - Python indent, for correcting python indents
    - reStructuredText, for writing documentation
    - Strict Whitespace, for ensuring no whitespace left in code
    - Python Docstring Generator, for writing docstring quickly
    - C/C++, for client development
    - Settings Sync, for syncing settings across remote servers