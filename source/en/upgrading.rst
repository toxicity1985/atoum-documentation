.. _upgrading:

Upgrading from v3 to v4
########################

atoum 4.0 was released in November 2020 and introduced several breaking changes. This guide will help you migrate your test suite from atoum 3.x to atoum 4.x.

.. contents:: Table of Contents
   :local:
   :depth: 2

.. _upgrading-requirements:

Requirements
************

PHP Version
===========

The most important requirement change is the PHP version:

.. list-table::
   :header-rows: 1
   :widths: 30 30 40

   * - atoum Version
     - PHP Version
     - Status
   * - 3.x
     - PHP 5.6 → 7.4
     - End of life
   * - 4.0 → 4.1
     - PHP 7.2 → 8.1
     - Supported
   * - 4.2+
     - PHP 8.0+
     - Current

**Action required:** Upgrade your PHP version to at least 8.0 (recommended) before upgrading to atoum 4.2+.

.. _upgrading-namespace:

Namespace Changes (Breaking Change)
***********************************

The most significant breaking change in atoum 4.0 is the namespace change.

Old Namespace (v3.x)
====================

.. code-block:: php

   <?php
   namespace vendor\project\tests\units;

   use mageekguy\atoum;

   class MyClass extends atoum\test
   {
       // ...
   }

New Namespace (v4.x)
====================

.. code-block:: php

   <?php
   namespace vendor\project\tests\units;

   use atoum\atoum;

   class MyClass extends atoum\test
   {
       // ...
   }

Migration Steps
===============

1. **Search and Replace**

   In all your test files, replace:

   - ``use mageekguy\atoum`` → ``use atoum\atoum``
   - ``mageekguy\atoum\`` → ``atoum\atoum\``

2. **Automated Script** (Linux/macOS)

   .. code-block:: bash

      # Backup your tests first!
      cp -r tests/ tests.backup/

      # Replace in all PHP files
      find tests/ -name "*.php" -type f -exec sed -i 's/mageekguy\\atoum/atoum\\atoum/g' {} \;
      find tests/ -name "*.php" -type f -exec sed -i 's/use mageekguy\\\\atoum/use atoum\\\\atoum/g' {} \;

3. **Verify Changes**

   Run your test suite to ensure everything still works:

   .. code-block:: bash

      vendor/bin/atoum

.. _upgrading-removed-features:

Removed Features
****************

IDE Extension
=============

The IDE extension has been removed from atoum's core in version 4.0.0.

**Before (v3.x):**

.. code-block:: php

   <?php
   // IDE extension was included in core
   $runner->addExtension(new \mageekguy\atoum\ide());

**After (v4.x):**

The IDE extension is no longer available in the core. If you need IDE integration, you'll need to find alternative solutions or community extensions.

**Action required:** Remove any references to the IDE extension from your configuration files.

Test Hooks
==========

The implementation of test hooks has been removed in atoum 4.0.0.

**Action required:** If you were using custom test hooks, you'll need to refactor your code to use alternative approaches such as:

- ``setUp()`` and ``tearDown()`` methods
- ``beforeTestMethod()`` and ``afterTestMethod()`` methods

.. _upgrading-composer:

Composer Update
***************

Update your ``composer.json``
==============================

.. code-block:: json

   {
       "require-dev": {
           "atoum/atoum": "^4.4"
       }
   }

Then run:

.. code-block:: bash

   composer update atoum/atoum

.. _upgrading-new-features:

New Features in v4.x
********************

Once you've migrated, you can take advantage of new features:

PHP 8.x Support
===============

atoum 4.x fully supports modern PHP features:

- **Static return type** (PHP 8.0) - Supported since atoum 4.1.0
- **Union types** (PHP 8.0) - Fully supported
- **Intersection types** (PHP 8.1) - Fully supported
- **Literal types** (null, true, false) (PHP 8.1) - Supported since atoum 4.2.0
- **readonly properties** (PHP 8.1) - Fully supported
- **Enums** (PHP 8.1) - Fully supported

See the :ref:`PHP 8.x Support section<mock_php8_support>` for more details.

Improved Mock Generator
=======================

The mock generator has been significantly improved to handle:

- Complex type declarations
- ``self``, ``parent``, and ``static`` return types (fixed in 4.4.1)
- Better compatibility with PHP 8.x features

.. _upgrading-testing:

Testing Your Migration
**********************

After migration, follow these steps to ensure everything works correctly:

1. **Run Your Test Suite**

   .. code-block:: bash

      vendor/bin/atoum

2. **Check for Deprecation Warnings**

   Look for any warnings about deprecated features that might have been missed.

3. **Verify Code Coverage**

   Ensure your code coverage reports are still generated correctly:

   .. code-block:: bash

      vendor/bin/atoum --enable-branch-and-path-coverage

4. **Test with Different PHP Versions**

   If you support multiple PHP versions, test with each:

   .. code-block:: bash

      # PHP 8.0
      php8.0 vendor/bin/atoum

      # PHP 8.1
      php8.1 vendor/bin/atoum

      # PHP 8.2
      php8.2 vendor/bin/atoum

.. _upgrading-troubleshooting:

Troubleshooting
***************

Common Issues
=============

**Issue: "Class 'mageekguy\atoum\test' not found"**

**Solution:** You missed some namespace changes. Search your codebase for ``mageekguy`` and replace with ``atoum\atoum``.

**Issue: "Composer cannot resolve dependencies"**

**Solution:** You might have other packages that depend on atoum 3.x. Update those packages first or check their compatibility with atoum 4.x.

**Issue: "Tests fail after migration"**

**Solution:** 
1. Check that all namespaces have been updated
2. Verify PHP version compatibility
3. Review removed features (IDE extension, test hooks)
4. Check your configuration files (``.atoum.php``)

Configuration File Example
==========================

Update your ``.atoum.php`` configuration file:

**Before (v3.x):**

.. code-block:: php

   <?php
   use mageekguy\atoum;

   $script->addDefaultReport();
   $runner->addTestsFromDirectory('tests/units');

**After (v4.x):**

.. code-block:: php

   <?php
   use atoum\atoum;

   $script->addDefaultReport();
   $runner->addTestsFromDirectory('tests/units');

.. _upgrading-help:

Getting Help
************

If you encounter issues during migration:

- Check the `CHANGELOG <https://github.com/atoum/atoum/blob/master/CHANGELOG.md>`_ for detailed information about changes
- Visit the `GitHub discussions <https://github.com/atoum/atoum/discussions>`_
- Open an issue on `GitHub <https://github.com/atoum/atoum/issues>`_ if you find a bug

.. _upgrading-checklist:

Migration Checklist
*******************

Use this checklist to track your migration progress:

.. code-block:: text

   ☐ Upgrade PHP to 8.0 or higher
   ☐ Update composer.json to require atoum ^4.4
   ☐ Run composer update
   ☐ Replace all mageekguy\atoum with atoum\atoum in test files
   ☐ Update .atoum.php configuration file
   ☐ Remove IDE extension references (if any)
   ☐ Refactor code using test hooks (if any)
   ☐ Run test suite and verify all tests pass
   ☐ Check code coverage reports
   ☐ Update CI/CD configuration if needed
   ☐ Update documentation/README
   ☐ Commit changes

.. note::
   The migration from v3 to v4 is straightforward for most projects. The main change is the namespace, which can be handled with a simple search and replace operation.

