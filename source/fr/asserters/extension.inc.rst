
.. _extension-anchor:

extension
*********

It's the asserter dedicated to PHP extension.

.. _extension-is-loaded:

isLoaded
========

Check if the extension is loaded (installed and enabled).

.. code-block:: php

	<?php
	$this
		->extension('json')
			->isLoaded()
		;

.. note::
	If you need to run tests only if an extension is present, you can use the :ref:`PHP annotation<annotation-php-extension>`.
