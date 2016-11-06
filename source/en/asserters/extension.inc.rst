
.. _extension-anchor:

extension
*********

It's the assertion dedicated to PHP extension.

.. _extension-is-loaded:

isLoaded
========

Test if the extension is loaded.

.. code-block:: php

	<?php
	$this
		->extension('json')
		->isLoaded()
		;

.. note::
	If you need to run tests only if an extension is present, you can use the :ref:`PHP annotation<annotation-php-extension>`.
