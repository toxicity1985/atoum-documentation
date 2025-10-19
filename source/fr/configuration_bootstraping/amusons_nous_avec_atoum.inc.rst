.. _fun-with-atoum:

Amusons-nous avec atoum
***********************

Rapport
=======

Les rapports de tests peuvent être décorés afin d'être plus agréables ou sympa à lire.
Pour cela, dans le :ref:`fichier de configuration <fichier-de-configuration>` d'atoum, ajoutez le code suivant

.. code-block:: php

	<?php
	// Le fichier de configuration par défaut est .atoum.php
	// ...

	$stdout = new \atoum\atoum\writers\std\out;
	$report = new \atoum\atoum\reports\realtime\nyancat;
	$script->addReport($report->addWriter($stdout));

Vous pouvez aussi essayer ``\atoum\atoum\reports\realtime\santa`` comme rapport ;)
