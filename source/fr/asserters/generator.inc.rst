.. _generator-anchor:

generator
*********

C'est l'asserter dédié aux tests sur les `generateurs <http://php.net/language.generators.overview>`_.

L'asserter ``generator`` hérite de l'asserter ``iterator``, vous pouvez donc utiliser toutes les assertions de cet asserter.

Example:

.. code-block:: php

   <?php
   $generator = function() {
       for ($i=0; $i<3; $i++) {
           yield ($i+1);
       }
   };
   $this
       ->generator($generator())
           ->hasSize(3)
   ;

Dans cet exemple, nous créons un générateur qui retourne 3 valeurs, et nous testons que la taille de ce générateur est bien 3.

.. _generator-yields:

yields
======

``yields`` est utilisé pour tester facilement les valeurs retournées par le générateur.
Chaque fois que vous appelez l'assertion ``->yields``, la prochaine valeur du générateur sera utilisée.
Vous aurez alors la possibilité d'utiliser l'asserter de votre choix sur la valeur retournée (par exemple ``class``, ``string`` or ``variable``).

Exemple:

.. code-block:: php

   <?php
   $generator = function() {
       for ($i=0; $i<3; $i++) {
           yield ($i+1);
       }
   };
   $this
       ->generator($generator())
           ->yields->variable->isEqualTo(1)
           ->yields->variable->isEqualTo(2)
           ->yields->integer->isEqualTo(3)
   ;

Dans cet exemple, nous créons un générateur qui retourne 3 valeurs : 1, 2 et 3.
Puis, pour chaque valeur du générateur, nous exécutons un test pour vérifier le type et la valeur.
Dans les 2 premiers tests, nous utilisons l'asserter ``variable`` pour vérifier uniquement la valeur.
Dans le troisième test, nous ajoutons un tests sur la valeur en utilisant l'asserter ``integer`` (tous les asserters peuvent être utilisée sur cette valeur) avant de tester la valeur.


.. _generator-returns:

returns
=======

.. note::
   Cette méthode ne fonctionne que pour PHP >= 7.0.


Depuis la version 7.0 de PHP, les générateurs peuvent retourner une valeur finale, qui peux être récupérée via un appel à la méthode ``->getReturn()``.
Lorsque vous utilisez l'assertion ``->returns`` sur l'asserter ``generator``, atoum vous permet d'exécuter des tests sur cette valeur de retour.

Exemple:

.. code-block:: php

   <?php
   $generator = function() {
       for ($i=0; $i<3; $i++) {
           yield ($i+1);
       }
       return 42;
   };
   $this
       ->generator($generator())
           ->yields->variable->isEqualTo(1)
           ->yields->variable->isEqualTo(2)
           ->yields->integer->isEqualTo(3)
           ->returns->integer->isEqualTo(42)
   ;

Dans cet exemple, nous commençons par exécuter plusieurs vérifications sur les valeurs retournées.
Puis, nous vérifions que la valeur de retour finale du générateur est bien un entier valant 42.
Comme lors de l'utilisation de l'assertion ``->yields``, vous pouvez utiliser tous les asserters pour valider la valeur de retour.

Historique
==========

+-----------+--------------------------------+
| Version   | Modifications                  |
+===========+================================+
| `v3.0.0`_ | Ajout de l'asserter generator. |
+-----------+--------------------------------+

.. _v3.0.0: https://github.com/atoum/atoum/blob/master/CHANGELOG.md#300---2017-02-22
