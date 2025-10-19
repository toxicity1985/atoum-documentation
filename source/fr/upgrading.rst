.. _upgrading:

Migration de la v3 vers la v4
##############################

atoum 4.0 est sorti en novembre 2020 et a introduit plusieurs changements majeurs. Ce guide vous aidera à migrer votre suite de tests d'atoum 3.x vers atoum 4.x.

.. contents:: Table des matières
   :local:
   :depth: 2

.. _upgrading-requirements:

Prérequis
*********

Version PHP
===========

Le changement de prérequis le plus important concerne la version de PHP :

.. list-table::
   :header-rows: 1
   :widths: 30 30 40

   * - Version atoum
     - Version PHP
     - Statut
   * - 3.x
     - PHP 5.6 → 7.4
     - Fin de vie
   * - 4.0 → 4.1
     - PHP 7.2 → 8.1
     - Supportée
   * - 4.2+
     - PHP 8.0+
     - Actuelle

**Action requise :** Mettez à jour votre version de PHP vers au moins 8.0 (recommandé) avant de migrer vers atoum 4.2+.

.. _upgrading-namespace:

Changement de namespace (Breaking Change)
******************************************

Le changement le plus significatif dans atoum 4.0 est le changement de namespace.

Ancien namespace (v3.x)
=======================

.. code-block:: php

   <?php
   namespace vendor\project\tests\units;

   use mageekguy\atoum;

   class MyClass extends atoum\test
   {
       // ...
   }

Nouveau namespace (v4.x)
========================

.. code-block:: php

   <?php
   namespace vendor\project\tests\units;

   use atoum\atoum;

   class MyClass extends atoum\test
   {
       // ...
   }

Étapes de migration
===================

1. **Rechercher et remplacer**

   Dans tous vos fichiers de test, remplacez :

   - ``use mageekguy\atoum`` → ``use atoum\atoum``
   - ``mageekguy\atoum\`` → ``atoum\atoum\``

2. **Script automatisé** (Linux/macOS)

   .. code-block:: bash

      # Sauvegardez d'abord vos tests !
      cp -r tests/ tests.backup/

      # Remplacer dans tous les fichiers PHP
      find tests/ -name "*.php" -type f -exec sed -i 's/mageekguy\\atoum/atoum\\atoum/g' {} \;
      find tests/ -name "*.php" -type f -exec sed -i 's/use mageekguy\\\\atoum/use atoum\\\\atoum/g' {} \;

3. **Vérifier les changements**

   Exécutez votre suite de tests pour vous assurer que tout fonctionne :

   .. code-block:: bash

      vendor/bin/atoum

.. _upgrading-removed-features:

Fonctionnalités supprimées
***************************

Extension IDE
=============

L'extension IDE a été retirée du core d'atoum dans la version 4.0.0.

**Avant (v3.x) :**

.. code-block:: php

   <?php
   // L'extension IDE était incluse dans le core
   $runner->addExtension(new \mageekguy\atoum\ide());

**Après (v4.x) :**

L'extension IDE n'est plus disponible dans le core. Si vous avez besoin d'une intégration IDE, vous devrez trouver des solutions alternatives ou des extensions communautaires.

**Action requise :** Supprimez toutes les références à l'extension IDE de vos fichiers de configuration.

Hooks de test
=============

L'implémentation des hooks de test a été supprimée dans atoum 4.0.0.

**Action requise :** Si vous utilisiez des hooks de test personnalisés, vous devrez refactoriser votre code pour utiliser des approches alternatives telles que :

- Les méthodes ``setUp()`` et ``tearDown()``
- Les méthodes ``beforeTestMethod()`` et ``afterTestMethod()``

.. _upgrading-composer:

Mise à jour avec Composer
**************************

Mettre à jour votre ``composer.json``
======================================

.. code-block:: json

   {
       "require-dev": {
           "atoum/atoum": "^4.4"
       }
   }

Puis exécutez :

.. code-block:: bash

   composer update atoum/atoum

.. _upgrading-new-features:

Nouvelles fonctionnalités de la v4.x
*************************************

Une fois la migration effectuée, vous pouvez profiter des nouvelles fonctionnalités :

Support PHP 8.x
===============

atoum 4.x supporte pleinement les fonctionnalités modernes de PHP :

- **Type de retour static** (PHP 8.0) - Supporté depuis atoum 4.1.0
- **Types union** (PHP 8.0) - Entièrement supportés
- **Types intersection** (PHP 8.1) - Entièrement supportés
- **Types littéraux** (null, true, false) (PHP 8.1) - Supportés depuis atoum 4.2.0
- **Propriétés readonly** (PHP 8.1) - Entièrement supportées
- **Enums** (PHP 8.1) - Entièrement supportés

Consultez la section :ref:`Support PHP 8.x<mock_php8_support>` pour plus de détails.

Générateur de mock amélioré
============================

Le générateur de mock a été considérablement amélioré pour gérer :

- Les déclarations de types complexes
- Les types de retour ``self``, ``parent`` et ``static`` (corrigés dans 4.4.1)
- Une meilleure compatibilité avec les fonctionnalités PHP 8.x

.. _upgrading-testing:

Tester votre migration
***********************

Après la migration, suivez ces étapes pour vous assurer que tout fonctionne correctement :

1. **Exécutez votre suite de tests**

   .. code-block:: bash

      vendor/bin/atoum

2. **Vérifiez les avertissements de dépréciation**

   Recherchez les avertissements concernant les fonctionnalités dépréciées qui auraient pu être manquées.

3. **Vérifiez la couverture de code**

   Assurez-vous que vos rapports de couverture de code sont toujours générés correctement :

   .. code-block:: bash

      vendor/bin/atoum --enable-branch-and-path-coverage

4. **Testez avec différentes versions de PHP**

   Si vous supportez plusieurs versions de PHP, testez avec chacune :

   .. code-block:: bash

      # PHP 8.0
      php8.0 vendor/bin/atoum

      # PHP 8.1
      php8.1 vendor/bin/atoum

      # PHP 8.2
      php8.2 vendor/bin/atoum

.. _upgrading-troubleshooting:

Dépannage
*********

Problèmes courants
==================

**Problème : "Class 'mageekguy\atoum\test' not found"**

**Solution :** Vous avez manqué certains changements de namespace. Recherchez ``mageekguy`` dans votre code et remplacez par ``atoum\atoum``.

**Problème : "Composer cannot resolve dependencies"**

**Solution :** Vous avez peut-être d'autres packages qui dépendent d'atoum 3.x. Mettez à jour ces packages en premier ou vérifiez leur compatibilité avec atoum 4.x.

**Problème : "Les tests échouent après la migration"**

**Solution :** 
1. Vérifiez que tous les namespaces ont été mis à jour
2. Vérifiez la compatibilité de la version PHP
3. Passez en revue les fonctionnalités supprimées (extension IDE, hooks de test)
4. Vérifiez vos fichiers de configuration (``.atoum.php``)

Exemple de fichier de configuration
====================================

Mettez à jour votre fichier de configuration ``.atoum.php`` :

**Avant (v3.x) :**

.. code-block:: php

   <?php
   use mageekguy\atoum;

   $script->addDefaultReport();
   $runner->addTestsFromDirectory('tests/units');

**Après (v4.x) :**

.. code-block:: php

   <?php
   use atoum\atoum;

   $script->addDefaultReport();
   $runner->addTestsFromDirectory('tests/units');

.. _upgrading-help:

Obtenir de l'aide
*****************

Si vous rencontrez des problèmes pendant la migration :

- Consultez le `CHANGELOG <https://github.com/atoum/atoum/blob/master/CHANGELOG.md>`_ pour des informations détaillées sur les changements
- Visitez les `discussions GitHub <https://github.com/atoum/atoum/discussions>`_
- Ouvrez une issue sur `GitHub <https://github.com/atoum/atoum/issues>`_ si vous trouvez un bug

.. _upgrading-checklist:

Liste de contrôle pour la migration
************************************

Utilisez cette liste pour suivre votre progression de migration :

.. code-block:: text

   ☐ Mettre à jour PHP vers 8.0 ou supérieur
   ☐ Mettre à jour composer.json pour require atoum ^4.4
   ☐ Exécuter composer update
   ☐ Remplacer tous les mageekguy\atoum par atoum\atoum dans les fichiers de test
   ☐ Mettre à jour le fichier de configuration .atoum.php
   ☐ Supprimer les références à l'extension IDE (le cas échéant)
   ☐ Refactoriser le code utilisant les hooks de test (le cas échéant)
   ☐ Exécuter la suite de tests et vérifier que tous les tests passent
   ☐ Vérifier les rapports de couverture de code
   ☐ Mettre à jour la configuration CI/CD si nécessaire
   ☐ Mettre à jour la documentation/README
   ☐ Commiter les changements

.. note::
   La migration de la v3 vers la v4 est simple pour la plupart des projets. Le changement principal est le namespace, qui peut être géré avec une simple opération de recherche et remplacement.

