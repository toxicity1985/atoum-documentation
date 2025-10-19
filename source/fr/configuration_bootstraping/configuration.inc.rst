.. _fichier-de-configuration:

Fichier de configuration
************************

Le fichier de configuration vous permet de configurer comment atoum fonctionne.
Si vous nommez votre fichier de configuration ``.atoum.php``, atoum le chargera automatiquement si ce fichier se trouve dans le répertoire courant. Le paramètre ``-c`` est donc optionnel dans ce cas.

.. note::
   La configuration de atoum supporte l'héritage de fichier. Si vous avez un fichier ``.atoum.php`` dans le répertoire parent, il sera également chargé.
   Vous pouvez ainsi avoir un fichier de configuration par défaut afin d'avoir le mode loop ou debug activé par défaut.

.. _config-file-example:

Exemple existant
================

atoum fourni un fichier d'exemple basique. Suivant le type d’installation de atoum, il y a plusieurs façons de les voir :

Depuis une installation PHAR
----------------------------

Si vous utlisez l'archive PHAR, il faut les extraire en utilisant la commande suivante :

.. code-block:: shell

   php atoum.phar -er /path/to/destination/directory

Une fois l'extraction effectuée, vous devriez avoir dans le répertoire /path/to/destination/directory un répertoire nommé resources/configurations/runner.

Depuis une installation composer
--------------------------------

Dans le cas où vous utilisez atoum en ayant cloné le dépôt :ref:`installation-par-github` ou l'ayant installé via :ref:`installation-par-composer`, les modèles se trouvent dans ``/path/to/atoum/resources/configurations/runner``

.. _coverage-code-config:

Couverture du code
==================

Par défaut, si PHP dispose de l'extension `Xdebug <http://xdebug.org>`_, atoum indique en ligne de commande le taux de couverture du code par les tests venant d'être exécutés. Certains comportements de la couverture de code peuvent être adaptés via les :ref:`options de l'interface en ligne de commande<cli-options-coverage_reports>`.
 

Si le taux de couverture est de 100%, atoum se contente de l'indiquer. Mais dans le cas contraire, il affiche le taux de couverture globale ainsi que celui de chaque méthode de la classe testée sous la forme d'un pourcentage.

.. code-block:: shell

   $ php tests/units/classes/template.php
   > atoum version DEVELOPMENT by Frederic Hardy (/Users/fch/Atoum)
   > PHP path: /usr/local/bin/php
   > PHP version:
   => PHP 5.3.8 (cli) (built: Sep 21 2011 23:14:37)
   => Copyright (c) 1997-2011 The PHP Group
   => Zend Engine v2.3.0, Copyright (c) 1998-2011 Zend Technologies
   =>     with Xdebug v2.1.1, Copyright (c) 2002-2011, by Derick Rethans
   > atoum\atoum\tests\units\template...
   [SSSSSSSSSSSSSSSSSSSSSSSSSSS_________________________________][27/27]
   => Test duration: 15.63 seconds.
   => Memory usage: 8.25 Mb.
   > Total test duration: 15.63 seconds.
   > Total test memory usage: 8.25 Mb.
   > Code coverage value: 92.52%
   => Class atoum\atoum\template: 91.14%
   ==> atoum\atoum\template::setWith(): 80.00%
   ==> atoum\atoum\template::resetChildrenData(): 25.00%
   ==> atoum\atoum\template::addToParent(): 0.00%
   ==> atoum\atoum\template::unsetAttribute(): 0.00%
   => Class atoum\atoum\template\data: 96.43%
   ==> atoum\atoum\template\data::__toString(): 0.00%
   > Running duration: 2.36 seconds.
   Success (1 test, 27 methods, 485 assertions, 0 error, 0 exception) !

Il est cependant possible d'obtenir une représentation plus précise du taux de couverture du code par les tests, sous la forme d'un rapport au format HTML. Cela peut être
trouver dans `l'extension report <http://extensions.atoum.org/extensions/reports>`_.

.. _coverage-code-reports:

Rapport de couverture personnalisée
-----------------------------------

Dans ce répertoire, il y a, entre autre chose intéressante, un modèle de fichier de configuration pour atoum nommé ``coverage.php.dist`` qu'il vous faudra copier à l'emplacement de votre choix. Renommez le ``coverage.php``.

Une fois le fichier copié, il n'y a plus qu'à le modifier à l'aide de l'éditeur de votre choix afin de définir le répertoire dans lequel les fichiers HTML devront être générés ainsi que l'URL à partir de laquelle le rapport devra être accessible.

Par exemple :

.. code-block:: php

   $coverageField = new atoum\report\fields\runner\coverage\html(
       'Code coverage de mon projet',
       '/path/to/destination/directory'
   );

   $coverageField->setRootUrl('http://url/of/web/site');

.. note::
   Il est également possible de modifier le titre du rapport à l'aide du premier argument du constructeur de la classe ``atoum\atoum\report\fields\runner\coverage\html``.


Une fois ceci en place, vous avez simplement a utiliser le fichier de configuration (ou l'inclure dans le fichier de configuration) lorsque vous lancer les tests, comme ceci :

.. code-block:: shell

   $ ./bin/atoum -c path/to/coverage.php -d tests/units

Une fois les tests exécutés, atoum génèrera alors le rapport de couverture du code au format HTML dans le répertoire que vous aurez défini précédemment, et il sera lisible à l'aide du navigateur de votre choix.

.. note::
   Le calcul du taux de couverture du code par les tests ainsi que la génération du rapport correspondant peuvent ralentir de manière notable l'exécution des tests. Il peut être alors intéressant de ne pas utiliser systématiquement le fichier de configuration correspondant, ou bien de les désactiver temporairement à l'aide de l'argument -ncc.

.. _reports-using:

Utilisation de rapports standards
=================================

atoum est fourni avec de nombreux rapports standards : tap, xunit, html, cli, phing, vim, ...  Il y a aussi quelques :ref:`rapports funs<fun-with-atoum>`. Vous trouverez les plus importants ici.

.. note::
   Si vous souhaitez aller plus loin, il y a une `extension <http://extensions.atoum.org/extensions/reports>`_ dédiée aux rapports appelée ``reports-extension``.

.. _reports-configuration:

Configuration de rapports
-------------------------

.. _reports-configuration_path-branch:

Couverture des branches et chemins
''''''''''''''''''''''''''''''''''

Dans le fichier de configuration, vous pouvez activer la couverture des branches et chemins à l'aide de l'option ``enableBranchAndPathCoverage``. Cette action améliorera la qualité de la couverture du code car elle ne se limitera pas à vérifier qu'une fonction est appelée, mais également
que chaque branche l'est également.
Pour faire simple, si vous avez un ``if``, le rapport changera si vous cherchez le ``else``. Vous pouvez aussi l'activer via la ligne commande avec :ref:`l'option --epbc<cli-options-ebpc>`.

.. code-block:: php

   $script->enableBranchAndPathCoverage();

.. code-block:: shell

   => Class Foo\Bar: Line: 31.46%
   # avec la couverture des branches et chemins
   => Class Foo\Bar: Line: 31.46% Path: 1.50% Branch: 26.06%

Désactiver la couverture pour une classe
''''''''''''''''''''''''''''''''''''''''

Si vous souhaitez exclure certaines classes de la couverture de code, vous pouvez utiliser ``$script->noCodeCoverageForClasses(\myClass::class)``.

.. _report-html-basic:

Rapport HTML
------------

Par défaut, atoum fournit un rapport HTML basique. Pour un rapport plus avancé, vous pouvez utiliser reports-extension.

.. code-block:: php

   <?php
   $report = $script->addDefaultReport();
   $coverageField = new atoum\report\fields\runner\coverage\html('Your Project Name', __DIR__ . '/reports');
   // Remplacez cette url par l'url racine de votre site de couverture de code.
   $coverageField->setRootUrl('http://url/of/web/site');
   $report->addField($coverageField);

.. _reports-cli:

Rapport CLI
-----------

Le rapport CLI est celui qui s'affiche quand vous lancez le test. Ce rapport a quelques options de configuration disponibles

* hideClassesCoverageDetails: Désactive la couverture d'une classe.
* hideMethodsCoverageDetails: Désactive la couverture d'une méthode.

.. code-block:: php

   <?php
   $script->addDefaultReport() // les rapports par défaut incluent celui-ci
       ->hideClassesCoverageDetails()
       ->hideMethodsCoverageDetails();

Afficher le logo d'atoum
''''''''''''''''''''''''

.. code-block:: php

   <?php
   $report = $script->addDefaultReport();

   // Cette ligne ajoute le logo d'atoum à chaque exécution
   $report->addField(new atoum\report\fields\runner\atoum\logo());

   // Celle-ci va ajouter un logo vert ou rouge après chaque exécution en fonction du status de cette dernière
   $report->addField(new atoum\report\fields\runner\result\logo());

.. _report-treemap:

Rapport Treemap
---------------


.. code-block:: php

   <?php
   $report = $script->addDefaultReport();

   $coverageHtmlField = new atoum\report\fields\runner\coverage\html('Your Project Name', __DIR__ . '/reports');
   // Remplacez cette url par l'url racine de votre site de couverture de code.
   $coverageHtmlField->setRootUrl('http://url/of/web/site');
   $report->addField($coverageField);

   $coverageTreemapField = new atoum\report\fields\runner\coverage\treemap('Your project name', __DIR__ . '/reports');
   $coverageTreemapField
      ->setTreemapUrl('http://url/of/treemap')
      ->setHtmlReportBaseUrl($coverageHtmlField->getRootUrl());

   $report->addField($coverageTreemapField);

.. _notifications-anchor:

Notifications
=============

atoum est capable de vous prévenir lorsque les tests sont exécutés en utilisant plusieurs systèmes de notification : `Growl`_, `Mac OS X Notification Center`_, `Libnotify`_.


Growl
-----

Cette fonctionnalité nécessite la présence de l'exécutable ``growlnotify``. Pour vérifier s'il est disponible, utilisez la commande suivante :

.. code-block:: shell

   $ which growlnotify

Vous aurez alors le chemin de l'exécutable ou alors le message ``growlnotify not found`` s'il n'est pas installé.

Il suffit ensuite d'ajouter le code suivant à votre fichier de configuration :

.. code-block:: php

   <?php
   $images = '/path/to/atoum/resources/images/logo';

   $notifier = new \atoum\atoum\report\fields\runner\result\notifier\image\growl();
   $notifier
       ->setSuccessImage($images . DIRECTORY_SEPARATOR . 'success.png')
       ->setFailureImage($images . DIRECTORY_SEPARATOR . 'failure.png')
   ;

   $report = $script->AddDefaultReport();
   $report->addField($notifier, array(atoum\runner::runStop));


Mac OS X Notification Center
----------------------------

Cette fonctionnalité nécessite la présence de l'exécutable ``terminal-notifier``. Pour vérifier s'il est disponible, utilisez la commande suivante :

.. code-block:: shell

   $ which terminal-notifier

Vous aurez alors le chemin de l'exécutable ou alors le message ``terminal-notifier not found`` s'il n'est pas installé.

.. note::
   Rendez-vous sur `la page Github du projet <https://github.com/alloy/terminal-notifier>`_ pour obtenir plus d'information sur l'installation de ``terminal-notifier``.


Il suffit ensuite d'ajouter le code suivant à votre fichier de configuration :

.. code-block:: php

   <?php
   $notifier = new \atoum\atoum\report\fields\runner\result\notifier\terminal();

   $report = $script->AddDefaultReport();
   $report->addField($notifier, array(atoum\runner::runStop));

Sous OS X, vous avez la possibilité de définir une commande qui sera exécutée lorsque l'utilisateur cliquera sur la notification.

.. code-block:: php

   <?php
   $coverage = new atoum\report\fields\runner\coverage\html(
       'Code coverage',
       $path = sys_get_temp_dir() . '/coverage_' . time()
   );
   $coverage->setRootUrl('file://' . $path);

   $notifier = new \atoum\atoum\report\fields\runner\result\notifier\terminal();
   $notifier->setCallbackCommand('open file://' . $path . '/index.html');

   $report = $script->AddDefaultReport();
   $report
       ->addField($coverage, array(atoum\runner::runStop))
       ->addField($notifier, array(atoum\runner::runStop))
   ;

L'exemple ci-dessus montre comment ouvrir le rapport de couverture du code lorsque l'utilisateur clique sur la notification.


Libnotify
---------

Cette fonctionnalité nécessite la présence de l'exécutable ``notify-send``. Pour vérifier s'il est disponible, utilisez la commande suivante :

.. code-block:: shell

   $ which notify-send

Vous aurez alors le chemin de l'exécutable ou alors le message ``notify-send not found`` s'il n'est pas installé.

Il suffit ensuite d'ajouter le code suivant à votre fichier de configuration :

.. code-block:: php

   <?php
   $images = '/path/to/atoum/resources/images/logo';

   $notifier = new \atoum\atoum\report\fields\runner\result\notifier\image\libnotify();
   $notifier
       ->setSuccessImage($images . DIRECTORY_SEPARATOR . 'success.png')
       ->setFailureImage($images . DIRECTORY_SEPARATOR . 'failure.png')
   ;

   $report = $script->AddDefaultReport();
   $report->addField($notifier, array(atoum\runner::runStop));

.. _configuration-test:

Configuration du test
=====================
De nombreuses possibilités sont disponibles pour configurer comment atoum va exécuter le test. Vous pouvez utiliser les arguments en ligne de commande ou le fichier de configuration.
Un code simple valant une longue explication, l'exemple suivant devrait être explicite :

.. code-block:: php

   <?php
   $testGenerator = new atoum\test\generator();

   // répertoire contenant le test unitaire. (-d)
   $testGenerator->setTestClassesDirectory(__DIR__ . '/test/units');

   // le namespace du test unitaire.
   $testGenerator->setTestClassNamespace('your\project\namespace\tests\units');

   // le runner de votre test unitaire.
   $testGenerator->setRunnerPath('path/to/your/tests/units/runner.php');

   $script->getRunner()->setTestGenerator($testGenerator);
   // ou
   $runner->setTestGenerator($testGenerator);

Vous pouvez également définir le répertoire du test avec ``$runner->addTestsFromDirectory(path)``. atoum chargera toutes les classes qui puissent être testées présentes dans ce dossier tout comme vous pouvez faire
avec l'argument en ligne de commande :ref:`-d<cli-options-directories>`.

.. code-block:: php

   <?php
   $runner->addTestsFromDirectory(__DIR__ . '/test/units');
