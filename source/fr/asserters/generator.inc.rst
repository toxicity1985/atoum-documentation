.. _generator-anchor:

generator
*********

Il s'agit de l'asserter dédié aux `generators <http://php.net/language.generators.overview>`_.

L’asserter generator hérite l’asserter ``iterator``, vous pouvez donc utiliser toutes les assertions de celui-ci.

Exemple :

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

Dans cet exemple, nous créons un générateur qui générera 3 valeurs, et nous vérifierons que la taille de ce qui est généré est de 3.

.. _generator-yields:

yields
======

``yields`` est utilisé pour facilité les tests sur les valeurs générée par le générateur.
Chaque fois que ``->yields`` est appelé, la valeur suivante du générateur est récupérée.
Vous pouvez ensuite utiliser tout les asserter sur cette valeur (par exemple ``class``, ``string`` ou ``variable``).

Exemple :

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


Dans cette exemple nous créer un générateur qui produit 3 valeurs : 1, 2 et 3.
Ensuite nous produisons chaque valeurs et effectuons une assertion sur celle-ci pour vérifier le type et la valeur.
Dans les deux premières valeurs produite, nous utilisons l'asserter ``variable`` et nous ne vérifions que la valeur.
Avec la troisième valeur produite, nous vérifions qu'il s'agit bien d'un entier (toute asserter peut-être utiliser sur cette valeur) avant de vérifier la valeur.



.. _generator-returns:

returns
=======

.. note::
   Cette assertion ne fonctionne que avec PHP >= 7.0.

Depuis la version 7.0 de PHP, les générateurs peuvent retourner une valeur via un appel à la méthode ``->getReturn()``.
Lorsque vous appeler ``->returns`` sur le l'asserter generator, atoum va renvoyé la valeur via la méthode ``->getReturn()``sur l'asserter.
Ensuite vous pourrez utiliser n'importe quel autre asserter sur cette valeur comme avec l'assertion ``yields``.

Exemple :

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

Dans cet exemple, nous effectuons quelques vérifications sur toutes les valeurs produites.
On vérifie ensuite que le générateur renvoie un entier avec une valeur de 42 (tout comme un appel à l’assertion yields, vous pouvez utiliser n’importe quel asserter pour vérifier la valeur retournée).

.. versionadded:: 3.0.0
   `Asserter generator ajouté <https://github.com/atoum/atoum/blob/master/CHANGELOG.md#300---2017-02-22>`_
