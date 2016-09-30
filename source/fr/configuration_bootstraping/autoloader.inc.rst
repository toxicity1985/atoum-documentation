
.. _autoloader_file:

L'autoloader
************

Le fichier d'autoload (autoloader) est ce que vous allez utiliser pour définir comment atoum va trouver la classe à tester.

Le nom du fichier par défaut est ``.autoloader.atoum.php``. Atoum le chargera automatiquement s'il se trouve dans le dossier courant.
Vous pouvez le redéfinir en ligne de commande avec les options ``--autoloader-file`` ou ``-af`` (:ref:`see the cli options<cli-options-autoloader_file>`).

Si l'autoloader n'existe pas, atoum essayera de charger le fichier ``vendor/autoload.php`` de composer. Vous n'aurez donc rien à faire dans la majorité des cas. ;)
