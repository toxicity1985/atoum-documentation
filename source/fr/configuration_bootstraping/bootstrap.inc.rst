
.. _bootstrap_file:

Fichier de bootstrap
**************

atoum autorise la définition d'un fichier de ``bootstrap`` qui sera exécuté avant chaque méthode de test et qui permet donc d'initialiser l'environnement d'exécution des tests.

Le nom par défaut du fichier est ``.bootstrap.atoum.php``, atoum chargera le fichier automatiquement, si celui-ci est situé dans le répertoire courant. Vous pouvez le définir en cli avec ``-bf`` ou ``--bootstrap-file``.

Il devient ainsi possible de définir, par exemple, de lire un fichier de configuration ou de réaliser toute autre opération nécessaire à la bonne exécution des tests.

La définition de ce fichier de bootstrap peut se faire de deux façons différentes, soit en ligne de commande, soit via un fichier de configuration.

.. code-block:: shell

   $ ./bin/atoum -bf path/to/bootstrap/file

.. note::
   Le fichier de bootstrap n'est pas un :ref:`fichier de configuration<fichier-de-configuration>` et , n'as pas les même possibilités.

Dans un fichier de configuration, atoum est configurable via la variable ``$runner``, qui n'est pas définie dans un fichier de ``bootstrap``.

De plus, ils ne sont pas inclus au même moment, puisque le fichier de configuration est inclus par atoum avant le début de l'exécution des tests mais après le lancement des tests, alors que le fichier de ``bootstrap``, s'il est défini, est le tout premier fichier inclus par atoum proprement dit. Enfin, le fichier de ``bootstrap`` peut permettre de ne pas avoir à inclure systématiquement le fichier ``scripts/runner.php`` ou l'archive PHAR de atoum dans les classes de test.
Cependant, dans ce cas, il ne sera plus possible d'exécuter directement un fichier de test directement via l'exécutable PHP en ligne de commande.
Pour cela, il suffit d'inclure dans le fichier de ``bootstrap`` le fichier ``scripts/runner.php`` ou l'archive PHAR d’atoum et d'exécuter systématiquement les tests en ligne de commande via ``scripts/runner.php`` ou l'archive PHAR.

Le fichier de ``bootstrap`` doit donc au minimum contenir ceci :

.. code-block:: php

   <?php

   // si l'archive PHAR est utilisée :
   require_once path/to/atoum.phar;

   // ou si vous voulez charger le $runner
   // require_once path/atoum/scripts/runner.php
