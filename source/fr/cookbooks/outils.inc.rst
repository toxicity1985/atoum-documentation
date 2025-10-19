
.. _cookbook_utilisation_behat:

Utilisation dans behat
**********************

Les *asserters* d'atoum sont très facilement utilisables hors de vos tests unitaires classiques. Il vous suffit d'importer la classe *atoum\atoum\asserter* en n'oubliant pas d'assurer le chargement des classes nécessaires (atoum fournit une classe d'autoload disponible dans *classes/autoloader.php*).
L'exemple suivant illustre cette utilisation des asserters atoum à l'intérieur de vos *steps* Behat.

Installation
============

Installez simplement atoum et Behat dans votre projet via pear, git clone, zip... Voici un exemple avec le gestionnaire de dépendances *Composer* :

.. code-block:: json

   "require-dev": {
           "behat/behat": "2.4@stable",
           "atoum/atoum": "~2.5"
   }

Il est évidemment nécessaire de remettre à jour vos dépendances composer en lançant la commande :

.. code-block:: shell

   $ php composer.phar update


Configuration
=============

Comme mentionné en introduction, il suffit d'importer la classe d'asserter et d'assurer le chargement des classes d'atoum. Pour Behat, la configuration des asserters s'effectue dans votre classe *FeatureContext.php* (située par défaut dans le répertoire */RACINE DE VOTRE PROJET/features/bootstrap/*).

.. code-block:: php

   <?php

   use Behat\Behat\Context\ClosuredContextInterface,
       Behat\Behat\Context\TranslatedContextInterface,
       Behat\Behat\Context\BehatContext,
       Behat\Behat\Exception\PendingException,
       Behat\Behat\Context\Step;
   use Behat\Gherkin\Node\PyStringNode,
       Behat\Gherkin\Node\TableNode;

   use atoum\asserter; // <- atoum asserter

   require_once __DIR__ . '/../../vendor/atoum/atoum/classes/autoloader.php'; // <- autoload

   class FeatureContext extends BehatContext
   {
       private $assert;

       public function __construct(array $parameters)
       {
           $this->assert = new asserter\generator();
       }
   }


Utilisation
===========

Après ces 2 étapes particulièrement triviales, vos *steps* peuvent s'enrichir des asserters atoum :

.. code-block:: php

   <?php

   // ...

   class FeatureContext extends BehatContext
   {//...

       /**
        * @Then /^I should get a good response using my favorite "([^"]*)"$/
        */
       public function goodResponse($contentType)
       {
           $this->assert
               ->integer($response->getStatusCode())
                   ->isIdenticalTo(200)
               ->string($response->getHeader('Content-Type'))
                   ->isIdenticalTo($contentType);
       }
   }

Encore une fois, ceci n'est qu'un exemple spécifique à Behat mais il reste valable pour tous les besoins d'utilisation des asserters d'atoum hors contexte initial.



.. _cookbook_utilisation_ci:

Utilisation dans des outils d'intégration continue (CI)
*******************************************************

.. _cookbook_utilisation_jenkins:

Utilisation dans Jenkins (ou Hudson)
====================================

Il est très simple d'intégrer les résultats de tests atoum à `Jenkins <http://jenkins-ci.org/>`_ (ou `Hudson <http://hudson-ci.org/>`_) en tant que résultats xUnit.


Étape 1 : Ajout d'un rapport xUnit à la configuration atoum
-----------------------------------------------------------

Comme pour les autres rapports de couverture, vous pouvez définir des :ref:`rapports spécifiques<reports-using>` dans la configuration.

Si vous n'avez pas de fichier de configuration
""""""""""""""""""""""""""""""""""""""""""""""

Si vous ne disposez pas encore d'un fichier de configuration pour atoum, nous vous recommandons d'extraire le répertoire ressource d’atoum dans celui de votre choix à l'aide de la commande suivante :

* Si vous utilisez l'archive Phar d'atoum :

.. code-block:: shell

   $ php atoum.phar --extractRessourcesTo /tmp/atoum-src
   $ cp /tmp/atoum-src/resources/configurations/runner/xunit.php.dist /mon/projet/.atoum.php

* Si vous utilisez les sources d'atoum :

.. code-block:: shell

   $ cp /chemin/vers/atoum/resources/configurations/runner/xunit.php.dist /mon/projet/.atoum.php

* Vous pouvez également copier le fichier directement `depuis le dépôt Github <https://github.com/atoum/atoum/blob/master/resources/configurations/runner/xunit.php.dist>`_

Il ne vous reste plus qu'à éditer ce fichier pour choisir l'emplacement où atoum génèrera le rapport xUnit. Ce fichier est prêt à l'emploi, avec lui, vous conservez le rapport par défaut d'atoum et vous obtiendrez un rapport xUnit à la suite de chaque lancement des tests.


Si vous avez déjà un fichier de configuration
"""""""""""""""""""""""""""""""""""""""""""""

Si vous disposez déjà d'un fichier de configuration, il vous suffit d'y ajouter les lignes suivantes :

.. code-block:: php

   <?php

   //...

   /*
    * Xunit report
    */
   $xunit = new atoum\reports\asynchronous\xunit();
   $runner->addReport($xunit);

   /*
    * Xunit writer
    */
   $writer = new atoum\writers\file('/chemin/vers/le/rapport/atoum.xunit.xml');
   $xunit->addWriter($writer);


Étape 2 : Tester la configuration
---------------------------------

Pour tester cette configuration, il suffit de lancer atoum en lui précisant le fichier de configuration que vous souhaitez utiliser :

.. code-block:: shell

   $ ./bin/atoum -d /chemin/vers/les/tests/units -c /chemin/vers/la/configuration.php

.. note::
   Si vous avez nommé votre fichier de configuration ``.atoum.php``, atoum le chargera automatiquement. Le paramètre ``-c`` est donc optionnel dans ce cas.
   Pour qu'atoum charge automatiquement ce fichier, vous devrez lancer les tests à partir du dossier où se trouve le fichier ``.atoum.php`` ou d'un de ses enfants.

À la fin de l'exécution des tests, vous devriez voir le rapport xUnit dans le répertoire indiqué dans le fichier de configuration.


Étape 3 : Lancement des tests via Jenkins (ou Hudson)
-----------------------------------------------------

Il existe pour cela plusieurs possibilités selon la façon dont vous construisez votre projet :

* Si vous utilisez un script, il vous suffit d'y ajouter la commande précédente.
* Si vous passez par un utilitaire tel que `phing <https://www.phing.info/>`_ ou `ant <http://ant.apache.org/>`_, il suffit d'ajouter une tâche exec :

.. code-block:: xml

   <target name="unitTests">
     <exec executable="/usr/bin/php" failonerror="yes" failifexecutionfails="yes">
       <arg line="/path/to/atoum.phar -p /path/to/php -d /path/to/test/folder -c /path/to/atoumConfig.php" />
     </exec>
   </target>

Vous noterez l'ajout du paramètre ``-p /chemin/vers/php`` qui permet d'indiquer à atoum le chemin vers le binaire PHP qu'il doit utiliser pour exécuter les tests unitaires.


Étape 4 : Publier le rapport avec Jenkins (ou Hudson)
-----------------------------------------------------

Il suffit tout simplement d'activer la publication des rapports au format JUnit ou xUnit, en fonction du plug-in que vous utilisez, en lui indiquant le chemin d'accès au fichier généré par atoum.



.. _cookbook_utilisation_travis-ci:

Utilisation avec Travis-ci
==========================

Il est assez simple d'utiliser atoum dans l'outil qu'est `Travis-CI <https://travis-ci.org>`__. En effet, l'ensemble des étapes est indiqué dans la `documentation de travis <http://docs.travis-ci.com/user/languages/php/#Working-with-atoum>`__ :
* Créer votre fichier .travis.yml dans votre projet;
* Ajoutez-y les deux lignes suivantes :

.. code-block:: yaml

   before_script: wget http://downloads.atoum.org/nightly/atoum.phar
   script: php atoum.phar


Voici un exemple de fichier `.travis.yml` dont les tests présents dans le dossier `tests` seront exécuter.

.. code-block:: yaml

   language: php
   php:
     - 5.4
     - 5.5
     - 5.6

   before_script: wget http://downloads.atoum.org/nightly/atoum.phar
   script: php atoum.phar -d tests/


.. _cookbook_utilisation_phing:

Utilisation avec `Phing <https://www.phing.info/>`_
***************************************************

La suite de tests de atoum peut facilement être exécutée au sein de votre configuration phing via l'intégration de la tâche *phing/AtoumTask.php*.
Un exemple valide peut être trouvé dans le fichier `resources/phing/build.xml <https://github.com/atoum/atoum/blob/master/resources/phing/build.xml>`_.

Vous devez néanmoins enregistrer votre tâche personnalisée en utilisant `taskdef <https://www.phing.info/docs/guide/stable/TaskdefTask.html>`_ , une tâche native de phing :

.. code-block:: xml

  <taskdef name="atoum" classpath="vendor/atoum/atoum/resources/phing" classname="AtoumTask"/>

Ensuite vous pouvez l’utiliser à l’intérieur de l’une de vos étapes du fichier de build :

.. code-block:: xml

    <target name="test">
      <atoum
        atoumautoloaderpath="vendor/atoum/atoum/classes/autoloader.php"
        phppath="/usr/bin/php"
        codecoverage="true"
        codecoveragereportpath="reports/html/"
        showcodecoverage="true"
        showmissingcodecoverage="true"
        maxchildren="5"
      >
        <fileset dir="tests/units/">
          <include name="**/*.php"/>
        </fileset>
      </atoum>
    </target>

Les chemins donnés dans cet exemple a été pris à partir d’une installation standard via composer. Tous les paramètres possibles
sont définis ci-dessous, vous pouvez modifier les valeurs ou en omettre certains et hériter des valeurs par défaut. Il y a trois types de paramètres :

Configuration d'atoum
=====================

- :ref:`bootstrap<bootstrap_file>`: fichier de bootstrap à inclure, exécuté avant chaque méthode de test

  - default: ``.bootstrap.atoum.php``
- :ref:`atoumpharpath<archive-phar>`: si atoum est utilisé au travers d'un phar, chemin vers celui-ci
- :ref:`atoumautoloaderpath<autoloader_file>`: fichier d'autoloader, le fichier est exécuté avant chaque méthode de test

  - default: ``.autoloader.atoum.php``
- :ref:`phppath<cli-options-php>`: chemin vers l'exécutable ``php``
- :ref:`maxchildren<cli-options-max_children_number>`: nombre maximum de sous-process qui peuvent tourner simultanément

Flags
=====

- `codecoverage`: active la couverture de code(uniquement si XDebug est disponible)

  - default: ``false``
- `showcodecoverage`: montre le rapport de couverture de code

  - default: ``true``
- `showduration`: montre la durée de l'exécution des tests

  - default: ``true``
- `showmemory`: affiche la consommation mémoire

  - default: ``true``
- `showmissingcodecoverage`: montre la couverture de code manquante

  - default: ``true``
- `showprogress`: affiche la barre de progression de l'exécution des tests

  - default: ``true``
- `branchandpathcoverage`: active la couverture de code sur les chemins et branches

  - default: ``false``
- `telemetry <http://extensions.atoum.org/extensions/telemetry>`_: active le rapport telemetry (l'extension `atoum/reports-extension` doit être installée)

  - default: ``false``

Rapports
========

- `codecoveragexunitpath`: chemin vers le rapport xunit
- `codecoveragecloverpath`: chemin vers le rapport clover
- :ref:`Couverture de code basic<report-html-basic>`

  - `codecoveragereportpath`: chemin vers le rapport html
  - `codecoveragereporturl`: url dans le rapport HTML
- :ref:`Couverture de code treemap<report-treemap>`:

  - `codecoveragetreemappath`: chemin vers le rapport treemap
  - `codecoveragetreemapurl`: url pour le treemap
- `Couverture de code avancée <http://extensions.atoum.org/extensions/reports>`_

  - `codecoveragereportextensionpath`: chemin vers le rapport html
  - `codecodecoveragereportextensionurl`: url du rapport HTML
- `Telemetry <http://extensions.atoum.org/extensions/telemetry>`_

  - `telemetryprojectname`: nom du projet a envoyer à telemetry
