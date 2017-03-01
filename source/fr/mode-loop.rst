
.. _mode-loop:

Mode répétition
###############

Lorsqu'un développeur fait du développement piloté par les tests, il travaille généralement de la manière suivante :

#. il commence par créer le test correspondant à ce qu'il veut développer ;
#. il exécute ensuite le test qu'il vient de créer ;
#. il écrit le code permettant au test de passer avec succès ;
#. il modifie ou complète son test et repars à l'étape 2.

Concrètement, cela signifie qu'il doit :

* créer son code dans son éditeur favori ;
* quitter son éditeur puis exécuter son test dans une console ;
* revenir à son éditeur pour écrire le code permettant au test de passer avec succès ;
* revenir à la console afin de relancer l'exécution de son test ;
* revenir à son éditeur afin de modifier ou compléter son test ;

Il y a donc un cycle qui se répète jusqu'à ce que la fonctionnalité soit terminée.

Au cours de ce cycle, le développeur doit à plusieurs reprises exécuter la même commande pour exécuter les tests unitaires.

atoum propose le mode ``loop`` disponible via les arguments ``-l`` ou ``--loop``, qui permet au développeur de ne pas avoir à relancer manuellement les tests et permet donc de fluidifier le processus de développement.

Dans ce mode, atoum exécute les tests demandés.

Une fois les tests terminés, si les tests ont été passés avec succès, atoum se met simplement en attente :

.. code-block:: shell

   $ php tests/units/classes/adapter.php -l
   > PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [SS__________________________________________________________][2/2]
   => Test duration: 0.00 second.
   => Memory usage: 0.50 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.50 Mb.
   > Running duration: 0.05 second.
   Success (1 test, 2/2 methods, 0 void method, 0 skipped method, 4 assertions)!
   Press <Enter> to reexecute, press any other key and <Enter> to stop...


Si le développeur presse la touche ``Enter``, atoum réexécutera à nouveau les mêmes tests, sans aucune autre action de la part du développeur.

Dans le cas où le code ne passe pas les tests avec succès, c'est-à-dire si les assertions échouent ou s'il y a des erreurs ou des exceptions, atoum se remet en mode d'attente :

.. code-block:: shell

   $ php tests/units/classes/adapter.php -l> PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [FS__________________________________________________________][2/2]
   => Test duration: 0.00 second.
   => Memory usage: 0.25 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.25 Mb.
   > Running duration: 0.05 second.
   Failure (1 test, 2/2 methods, 0 void method, 0 skipped method, 0 uncompleted method, 1 failure, 0 error, 0 exception)!
   > There is 1 failure:
   => mageekguy\atoum\tests\units\adapter::test__call():
   In file /media/data/dev/atoum-documentation/tests/vendor/atoum/atoum/tests/units/classes/adapter.php on line 16, mageekguy\atoum\asserters\string() failed: strings are not equal
   -Expected
   +Actual
   @@ -1 +1 @@
   -string(32) "1305beaa8f3f2f932f508d4af7f89094"
   +string(32) "d905c0b86bf89f9a57d4da6101f93648"
   Press <Enter> to reexecute, press any other key and <Enter> to stop...


Si le développeur presse la touche ``Enter``, au lieu de rejouer les mêmes tests, atoum n'exécutera que les tests en échec, au lieu de rejouer l'ensemble.

Le développeur pourra alors dépiler les problèmes et rejouer les tests en erreur autant de fois que nécessaire simplement en appuyant sur ``Enter``.

De plus, une fois que tous les tests en échec passeront à nouveau avec succès, atoum exécutera automatiquement la totalité de la suite de tests afin de détecter les éventuelles régressions introduites par la ou les corrections effectuées par le développeur.

.. code-block:: shell

   Press <Enter> to reexecute, press any other key and <Enter> to stop...
   > PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [S___________________________________________________________][1/1]
   => Test duration: 0.00 second.
   => Memory usage: 0.25 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.25 Mb.
   > Running duration: 0.05 second.
   Success (1 test, 1/1 method, 0 void method, 0 skipped method, 2 assertions)!
   > PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [SS__________________________________________________________][2/2]
   => Test duration: 0.00 second.
   => Memory usage: 0.50 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.50 Mb.
   > Running duration: 0.05 second.
   Success (1 test, 2/2 methods, 0 void method, 0 skipped method, 4 assertions)!
   Press <Enter> to reexecute, press any other key and <Enter> to stop...


Bien évidemment, le mode ``loop`` ne prend en compte que :ref:`le ou les fichiers de tests unitaires lancés <fichiers-a-executer>` par atoum.
