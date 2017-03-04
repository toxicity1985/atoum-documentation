
.. _data-provider:

Data providers
**************

Afin de permettre de tester efficacement vos classes, atoum fourni des data provider (fournisseur de données).

Un data provider est une méthode spécifique d'une classe de test chargée de générer des arguments pour une méthode de test, arguments qui seront utilisés par ladite méthode pour valider des assertions.

Si méthode de test ``testFoo`` prend des arguments, mais qu'aucune annotation précisant le data provider n'est présente, atoum va automatiquement rechercher une méthode ``testFooDataProvider``.

Vous pouvez également définir manuellement le nom de la méthode du data provider grâce à l'annotation ``@dataProvider`` à ajouter à la méthode de test :

.. code-block:: php

   <?php
   class calculator extends atoum
   {
       /**
        * @dataProvider sumDataProvider
        */
       public function testSum($a, $b)
       {
           $this
               ->if($calculator = new project\calculator())
               ->then
                   ->integer($calculator->sum($a, $b))->isEqualTo($a + $b)
           ;
       }

       // ...
   }

Bien évidemment, il faut penser a définir les arguments de la méthode de test qui vont recevoir les données retournées par le data provider. Dans le cas contraire, atoum va retourner des erreurs lors de l'exécution des tests.

Un data provider est une méthode protégée qui retourne un tableau ou un itérateur qui contient de simples valeurs :

.. code-block:: php

   <?php
   class calculator extends atoum
   {
       // ...

       // Fourni des données pour testSum().
       protected function sumDataProvider()
       {
           return array(
               array( 1, 1),
               array( 1, 2),
               array(-1, 1),
               array(-1, 2),
           );
       }
   }

Lors de l'exécution des test, atoum va appeler la méthode ``testSum()`` avec les arguments ``(1, 1)``, ``(1, 2)``, ``(-1, 1)`` et ``(-1, 2)``, tels que retournés par la méthode ``sumDataProvider()``.

.. warning::
   L'isolation des tests ne sera pas utilisée dans ce cas d'utilisation, ce qui signifie que les appels successifs à la méthode ``testSum()`` seront exécutés dans le même processus PHP.

.. _data-provider-closure:

Data provider en tant que closure
=================================

Vous pouvez également utiliser une closure pour définir un data provider au lieu d’une annotation. Dans votre méthode :ref:`beforeTestMethod<initialization_method>`, vous pouvez utiliser l'exemple suivant pour définir une closure :

.. code-block:: php

   <?php
   class calculator extends atoum
   {
      // ...
      public function beforeTestMethod($method)
      {
         if ($method == 'testSum')
         {
            $this->setDataProvider($method, function() {
              return array(
                  array( 1, 1),
                  array( 1, 2),
                  array(-1, 1),
                  array(-1, 2),
              );
            });
         }
      }
   }


.. _data-provider-injected:

Data provider injecté dans les méthode de test
==============================================

Il y a aussi, une injection de bouchon dans les paramètres de la méthode de test. Prenons un exemple simple :

.. code-block:: php

   <?php
   class cachingIterator extends atoum
   {
       public function test__construct()
       {
           $this
               ->given($iterator = new \mock\iterator())
               ->then
                   ->object($this->newTestedInstance($iterator))
           ;
       }
   }

Vous pouvez l'écrire ainsi :

.. code-block:: php

   <?php

   class cachingIterator extends atoum
   {
       public function test__construct(\iterator $iterator)
       {
           $this
               ->object($this->newTestedInstance($iterator))
           ;
       }
   }

Dans ce cas, pas besoin de data provider. Cependant, si vous désirez changer le comportement de vos bouchons, cela requiert l'utilisation de  :ref:`beforeTestMethod<initialization_method>`.

.. code-block:: php

   <?php

   class cachingIterator extends atoum
   {
       public function test__construct(\iterator $iterator)
       {
           $this
               ->object($this->newTestedInstance($iterator))
           ;
       }

       public function beforeTestMethod($method)
       {
           // rend le controlleur orphelin pour le prochain mock généré, ici $iterator
           $this->mockGenerator->orphanize('__construct');
       }
   }
