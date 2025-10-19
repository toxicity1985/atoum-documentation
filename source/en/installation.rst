
.. _installation:

Installation
************

If you want to use atoum, simply download the latest version.

.. _installation-requirements:

Requirements
============

atoum requires **PHP 8.0 or higher** to work.

Here is the compatibility table between PHP and atoum versions:

.. list-table::
   :header-rows: 1
   :widths: 30 30

   * - PHP Version
     - atoum Version
   * - 5.3 → 5.6
     - 1.x → 3.x
   * - 7.2 → 8.1
     - 4.0 → 4.1
   * - 8.0+
     - 4.1+ (current)

.. note::
   For PHP 8.0+, we recommend using the latest version of atoum via Composer to benefit from the latest features and bug fixes.

Installation methods
====================

You can install atom in several ways:

* using `composer`_;
* download the `PHAR archive`_;
* clone the `Github`_ repository;
* see also the :ref:`integration with your frameworks <utilisation-avec-frameworks>`.

.. _installation-par-composer:

Composer
========

`Composer <http://getcomposer.org>`_ is a dependency management tool in PHP.

Be sure you have a working `composer installation <https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx>`_.

Add ``atoum/atoum`` as a dev dependency :

.. code-block:: shell

   composer require --dev atoum/atoum


.. _archive-phar:

PHAR archive
============

.. warning::
	For the moment the phar build is broken, so this is not avilable....

A PHAR (PHp ARchive) is created automatically on each modification of atoum.

PHAR is an archive format for PHP application.


Installation
------------

You can download the latest stable version of atoum directly from the official website: `http://downloads.atoum.org/nightly/atoum.phar <http://downloads.atoum.org/nightly/atoum.phar>`_


Update
------

To update the PHAR archive, just run the following command:

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar --update

.. note::
	The update process modifies the PHAR archive. But the default PHP configuration doesn't allow this. So it is mandatory to use the directive ``-d phar.readonly=0``.


If a newer version is available it will be downloaded automatically and installed in the archive:

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar --update
   Checking if a new version is available... Done !
   Update to version 'nightly-2416-201402121146'... Done !
   Enable version 'nightly-2416-201402121146'... Done !
   Atoum was updated to version 'nightly-2416-201402121146' successfully !

If there is no newer version, atoum will stop immediately:

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar --update
   Checking if a new version is available... Done !
   There is no new version available !

atoum doesn't require any confirmation from the user to be upgraded, because it's very easy to get back to a previous version.

List the versions contained in the archive
------------------------------------------

You can list versions in the archive by using the argument ``--list-available-versions``, or ``-lav``:

.. code-block:: shell

   $ php atoum.phar -lav
     nightly-941-201201011548
     nightly-1568-201210311708
   * nightly-2416-201402121146

The list of versions in the archive is displayed. The currently active version is preceded by ``*``.

Change the current version
--------------------------

To activate another version, just use the argument ``--enable-version``, or ``-ev``, followed by the name of the version to use:

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar -ev DEVELOPMENT

.. note::
	Modification of the current version requires the modification of the PHAR archive. The default PHP configuration doesn't allow this. So it is mandatory to use the directive ``-d phar.readonly=0``.


Deleting older versions
-----------------------

Over time, the archive may contain multiple versions of atoum which are no longer required.

To remove them, just use the argument ``--delete-version``, or ``-dv`` followed by the name of the version to deleted:

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar -dv nightly-941-201201011548

The version is then removed.

.. warning::
	It's not possible to delete the current version.

.. note::
	Deleting a version requires the modification of the PHAR archive. the default PHP configuration doesn't allow this. 
	So it is mandatory to use the directive ``-d phar.readonly=0``.

.. _installation-par-github:

Github
======

If you want to use atoum directly from source code, you can clone or « fork » the github repository: git://github.com/atoum/atoum.git
