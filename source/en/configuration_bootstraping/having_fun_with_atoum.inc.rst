.. _fun-with-atoum:

Having fun with atoum
*********************

Report
======

Tests reports can be decorated to be more pleasant or fun to read.
To do this in the  :ref:`configuration file <fichier-de-configuration>` of atoum, add the following code

.. code-block:: php

	<?php
	// Default configuration file is .atoum.php
	// ...

	$stdout = new \atoum\atoum\writers\std\out;
	$report = new \atoum\atoum\reports\realtime\nyancat;
	$script->addReport($report->addWriter($stdout));

You should also try ``\atoum\atoum\reports\realtime\santa`` reports ;)
