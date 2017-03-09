
.. _extension-anchor:

extension
*********

C'est l'assertion dédiée aux extensions PHP.

.. _extension-is-loaded:

isLoaded
========

Vérifie si l’extension est chargée (installée et activée).

.. code-block:: php

	<?php
	$this
		->extension('json')
			->isLoaded()
		;

.. note::
	Si vous avez besoin de lancer un test uniquement si une extension est présente, vous pouvez utiliser :ref:`l'annotation PHP<annotation-php-extension>`.
