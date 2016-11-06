
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
	You can also use the tag :ref:`extension<annotation-php-extension>`, in some case.
