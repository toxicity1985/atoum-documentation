

.. _installation:

Installation
************

Si vous souhaitez utiliser atoum, il vous suffit de télécharger la dernière version.

.. _installation-requirements:

Prérequis
=========

atoum nécessite **PHP 8.0 ou supérieur** pour fonctionner.

Voici le tableau de compatibilité entre les versions de PHP et d'atoum :

.. list-table::
   :header-rows: 1
   :widths: 30 30

   * - Version PHP
     - Version atoum
   * - 5.3 → 5.6
     - 1.x → 3.x
   * - 7.2 → 8.1
     - 4.0 → 4.1
   * - 8.0+
     - 4.1+ (actuelle)

.. note::
   Pour PHP 8.0+, nous recommandons d'utiliser la dernière version d'atoum via Composer pour bénéficier des dernières fonctionnalités et corrections de bugs.

Méthodes d'installation
========================

Vous pouvez installer atoum de plusieurs manières :

* à l'aide de `composer`_ ;
* en téléchargeant l'`archive PHAR`_ ;
* en clonant le dépôt `Github`_ ;
* voir aussi :ref:`l'integration d'atoum dans votre framework <utilisation-avec-frameworks>`.

.. _installation-par-composer:

Composer
========

`Composer <http://getcomposer.org>`_ est un outil de gestion de dépendance en PHP.

Assurez-vous que vous disposez d'une installation de `composer fonctionnelle <https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx>`_

Ajoutez ``atoum/atoum`` à vos dépendances de développement :

.. code-block:: shell

   composer require --dev atoum/atoum


.. _archive-phar:

Archive PHAR
============


.. warning::
	Pour le moment, la construction du phar est cassé, du coup ce n'est pas possible pour le moment...

Une archive PHAR (PHp ARchive) est créée automatiquement à chaque modification d'atoum.

PHAR est un format d'archive applicative pour PHP.


Installation
------------

Vous pouvez télécharger la dernière version stable d'atoum directement depuis le site officiel : `http://downloads.atoum.org/nightly/atoum.phar <http://downloads.atoum.org/nightly/atoum.phar>`_


Mise à jour
-----------

Pour mettre à jour le PHAR, utiliser simplement la commande :

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar --update

.. note::
	Le processus de mise à jour modifie l'archive PHAR. Cependant, par défaut la configuration de PHP ne l'autorise pas. Voilà pourquoi il faut utiliser la directive ``-d phar.readonly=0``.


Si une version plus récente existe, elle sera alors téléchargée automatiquement et installée au sein de l'archive :

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar --update
   Checking if a new version is available... Done !
   Update to version 'nightly-2416-201402121146'... Done !
   Enable version 'nightly-2416-201402121146'... Done !
   Atoum was updated to version 'nightly-2416-201402121146' successfully !

S'il n'existe pas de version plus récente, atoum s'arrêtera immédiatement :

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar --update
   Checking if a new version is available... Done !
   There is no new version available !

atoum ne demande aucune confirmation de la part de l'utilisateur pour réaliser la mise à jour, car il est très facile de revenir à une version précédente.

Lister les versions contenues dans l'archive
--------------------------------------------

Vous pouvez lister les versions disponibles dans les archives en utilisant ``--list-available-versions`` ou ``-lav``:

.. code-block:: shell

   $ php atoum.phar -lav
     nightly-941-201201011548
     nightly-1568-201210311708
   * nightly-2416-201402121146

La liste des versions de l’archive est affichée. La version actuellement active est précédée par ``*``.

Changer la version courante
---------------------------

Pour activer une autre version, il suffit d'utiliser l'argument ``--enable-version``, ou ``-ev`` en version abrégée, suivi du nom de la version à utiliser :

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar -ev DEVELOPMENT

.. note::
	La modification de la version courante nécessite la modification de l'archive PHAR. Cependant, par défaut la configuration de PHP ne l'autorise pas. Voilà pourquoi il faut utiliser la directive ``-d phar.readonly=0``.


Suppression d'anciennes versions
--------------------------------

Au cours du temps, l'archive peut contenir plusieurs versions d'atoum qui ne sont plus utilisées.

Pour les supprimer, il suffit d'utiliser l'argument ``--delete-version``, ou ``-dv`` dans sa version abrégée, suivi du nom de la version à supprimer :

.. code-block:: shell

   $ php -d phar.readonly=0 atoum.phar -dv nightly-941-201201011548

La version est alors supprimée.

.. warning::
	Il n'est pas possible de supprimer la version active.

.. note::
	La suppression d'une version nécessite la modification de l'archive PHAR. par défaut la configuration de PHP ne l'autorise pas. 
	Voilà pourquoi il faut utiliser la directive ``-d phar.readonly=0``.

.. _installation-par-github:

Github
======

Si vous souhaitez utiliser atoum directement depuis ses sources, vous pouvez cloner ou « forker » le dépôt github : `git://github.com/atoum/atoum.git <git://github.com/atoum/atoum.git>`_
