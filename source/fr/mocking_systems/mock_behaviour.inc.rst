
.. _mock_behaviour_change:

Modifier le comportement d'un bouchon
******************************

Une fois le bouchon créé et instancié, il est souvent utile de pouvoir modifier le comportement de ses méthodes. Pour cela,
il faut passer par son contrôleur en utilisant l'une des méthodes suivantes :

* $yourMock->getMockController()->yourMethod
* $this->calling($yourMock)->yourMethod

.. code-block:: php

   <?php
   $mockDbClient = new \mock\Database\Client();

   $mockDbClient->getMockController()->connect = function() {};
   // Equivalent to
   $this->calling($mockDbClient)->connect = function() {};

Le ``mockController`` vous permet de redéfinir **uniquement les méthodes publiques et abstraites protégées** et met à votre disposition plusieurs méthodes :

.. code-block:: php

   <?php
   $mockDbClient = new \mock\Database\Client();

   // redéfinit la méthode connect : elle retournera toujours true
   $this->calling($mockDbClient)->connect = true;

   // redéfinit la méthode select : elle exécutera la fonction anonyme passée
   $this->calling($mockDbClient)->select = function() {
       return array();
   };

   // redéfinit la méthode query avec des arguments
   $result = array();
   $this->calling($mockDbClient)->query = function(Query $query) use($result) {
       switch($query->type) {
           case Query::SELECT:
               return $result;

           default;
               return null;
       }
   };

   // la méthode connect lèvera une exception
   $this->calling($mockDbClient)->connect->throw = new \Database\Client\Exception();

.. note::
	La syntaxe utilise les fonctions anonymes (aussi appelées fermetures ou closures) introduites en PHP 5.3. Reportez-vous
	au `manuel de PHP <http://php.net/functions.anonymous>`__ pour avoir plus d'informations sur le sujet.

Comme vous pouvez le voir, il est possible d'utiliser plusieurs méthodes afin d'obtenir le comportement souhaité :

* Utiliser une valeur statique qui sera retournée par la méthode
* Utiliser une implémentation courte grâce aux fonctions anonymes de PHP
* Utiliser le mot-clef ``throw`` pour lever une exception

Changement de comportement du mock sur plusieurs appels
=======================================================

Vous pouvez également spécifier plusieurs valeurs en fonction de l'ordre d'appel :

.. code-block:: php

   <?php
   // default
   $this->calling($mockDbClient)->count = rand(0, 10);
   // équivalent à
   $this->calling($mockDbClient)->count[0] = rand(0, 10);

   // 1er appel
   $this->calling($mockDbClient)->count[1] = 13;

   // 3ème appel
   $this->calling($mockDbClient)->count[3] = 42;

* Le premier appel retournera 13.
* Le second aura le comportement par défaut, c'est-à-dire un nombre aléatoire.
* Le troisième appel retournera 42.
* Tous les appels suivants auront le comportement par défaut, c'est à dire des nombres aléatoires.

Si vous souhaitez que plusieurs méthodes du bouchon aient le même comportement, vous pouvez utiliser les méthodes :ref:`methods<mock_methods>` ou :ref:`methodsMatching<mock_method_matching>`.




.. _mock_methods:

methods
=======

``methods`` vous permet, grâce à la fonction anonyme passée en argument, de définir pour quelles méthodes le comportement doit être modifié :

.. code-block:: php

   <?php
   // si la méthode a tel ou tel nom,
   // on redéfinit son comportement
   $this
       ->calling($mock)
           ->methods(
               function($method) {
                   return in_array(
                       $method,
                       array(
                           'getOneThing',
                           'getAnOtherThing'
                       )
                   );
               }
           )
               ->return = uniqid()
   ;

   // on redéfinit le comportement de toutes les méthodes
   $this
       ->calling($mock)
           ->methods()
               ->return = null
   ;

   // si la méthode commence par "get",
   // on redéfinit son comportement
   $this
       ->calling($mock)
           ->methods(
               function($method) {
                   return substr($method, 0, 3) == 'get';
               }
           )
               ->return = uniqid()
   ;


Dans le cas du dernier exemple, vous devriez plutôt utiliser :ref:`methodsMatching<mock_method_matching>`.

.. note::
	La syntaxe utilise les fonctions anonymes (aussi appelées fermetures ou closures) introduites en PHP 5.3. Reportez-vous
	au `manuel de PHP <http://php.net/functions.anonymous>`__ pour avoir plus d'informations sur le sujet.


.. _mock_method_matching:

methodsMatching
===============

``methodsMatching`` vous permet de définir les méthodes où le comportement doit être modifié grâce à l'expression
rationnelle passée en argument :

.. code-block:: php

   <?php
   // si la méthode commence par "is",
   // on redéfinit son comportement
   $this
       ->calling($mock)
           ->methodsMatching('/^is/')
               ->return = true
   ;

   // si la méthode commence par "get" (insensible à la casse),
   // on redéfinit son comportement
   $this
       ->calling($mock)
           ->methodsMatching('/^get/i')
               ->throw = new \exception
   ;

.. note::
	``methodsMatching`` utilise `preg_match <http://php.net/preg_match>`_ et les expressions rationnelles. Reportez-vous
	au `manuel de PHP <http://php.net/pcre>`__ pour avoir plus d'informations sur le sujet.

isFluent && returnThis
======================

Défini une méthode fluent (chaînable), ainsi la méthode appelée retourne l'instance de la classe.

.. code-block:: php

	<?php
		$foo = new \mock\foo();
		$this->calling($foo)->bar = $foo;

		// est identique à
		$this->calling($foo)->bar->isFluent;
		// ou a celui-ci
		$this->calling($foo)->bar->returnThis;

doesNothing && doesSomething
============================

Changer le comportement du mock avec ``doesNothing``, la méthode retournera simple null.

.. code-block:: php

	<?php
		class foo {
			public function bar() {
				return 'baz';
			}
		}

		//
		// in your test
		$foo = new \mock\foo();
		$this->calling($foo)->bar = null;

		// est identique à
		$this->calling($foo)->bar->doesNothing;
		$this->variable($foo->bar())->isNull;

		// restaure le comportement
		$this->calling($foo)->bar->doesSomething;
		$this->string($foo->bar())->isEqualTo('baz');

Comme on le voix dans l'exemple, si pour une raison quelconque, vous souhaitez rétablir le comportement de la méthode, utilisez ``doesSomething``.

.. _mock_special_constructor:

Cas particulier du constructeur
==================================

Pour mocker le constructeur de la classe, vous avez besoin de :

* créer une instance de la classe \atoum\mock\controller avant d'appeler le constructeur du bouchon ;
* définir via ce contrôleur le comportement du constructeur du bouchon à l'aide d'une fonction anonyme ;
* injecter le contrôleur lors de l'instanciation du bouchon en `dernier` argument.

.. code-block:: php

   <?php
   $controller = new \atoum\mock\controller();
   $controller->__construct = function($args)
   {
        // faire quelque chose avec les arguments
   };

   $mockDbClient = new \mock\Database\Client(DB_HOST, DB_USER, DB_PASS, $controller);

Pour les cas simple, vous pouvez utiliser :ref:`orphanize('__constructor')<mock_orphan_method>` ou :ref:`shunt('__constructor')<mock_shunt>`.
