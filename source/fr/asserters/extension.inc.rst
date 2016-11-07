
.. _extension-anchor:

extension
*********

C'est l'asserter dédiée aux extensions PHP.

.. _extension-is-loaded:

isLoaded
========

Vérifie si l'extension est installée et chargée.

.. code-block:: php

	<?php
	$this
		->extension('json')
			->isLoaded()
		;

.. note::
	Si vous devez exécuter certains tests uniquement dans le cas où une extension est présente, vous pouvez utiliser :ref:`l'annotation PHP<annotation-php-extension>`.
