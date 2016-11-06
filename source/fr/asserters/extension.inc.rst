
.. _extension-anchor:

extension
*********

C'est l'assertion dédiée aux extension PHP.

.. _extension-is-loaded:

isLoaded
========

Test si l'extension est chargée.

.. code-block:: php

	<?php
	$this
		->extension('json')
		->isLoaded()
		;

.. note::
	Si vous devez exécuté certains tests uniquement dans le cas où une extension est présente, vous pouvez utiliser :ref:`l'annotation PHP<annotation-php-extension>`.
