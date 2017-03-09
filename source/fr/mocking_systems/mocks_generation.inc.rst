
.. _mock_generate_one:

Générer un bouchon
***************

Il y a plusieurs manières de créer un bouchon à partir d'une interface ou d'une classe. Le plus simple est de créer un
objet avec le nom absolu préfixé de ``mock`` :

.. code-block:: php

   <?php
   // création d'un bouchon de l'interface \Countable
   $countableMock = new \mock\Countable;

   // création d'un bouchon de la classe abstraite
   // \Vendor\Project\AbstractClass
   $vendorAppMock = new \mock\Vendor\Project\AbstractClass;

   // creation of mock of the \StdClass class
   $stdObject     = new \mock\StdClass;

   // création d'un bouchon à partir d'une classe inexistante
   $anonymousMock = new \mock\My\Unknown\Claass;

.. _mock_generate_fast:

Générer un mock avec newMockInstance
====================================

Si vous préférez il existe une méthode ``newMockInstance()`` qui permet la génération d'un mock.

.. code-block:: php

   <?php
   // création d'un bouchon de l'interface \Countable
   $countableMock = new \mock\Countable;

   // est équivalent à
   $this->newMockInstance('Countable');

.. note::
	Comme le générateur de mock, vous pouvez fournir des paramètres en plus : ``$this->newMockInstance('class name', 'mock namespace', 'mock class name', ['constructor args']);``




.. _mock_generator:

Le générateur de bouchon
************************

atoum s'appuie sur un composant spécialisé pour générer les bouchons : le ``mockGenerator``.
Vous avez accès à ce dernier dans vos tests afin de modifier la procédure de génération des mocks.

Par défaut, le mock sera généré dans le namespace "mock" et fonctionnera exactement de la même manière que
l'instance de la classe originale (le mock hérite directement de la classe d'origine).

.. _mock_change_name:

Changer le nom de la classe
===========================

Si vous désirez changer le nom de la classe ou son espace de nom, vous devez utiliser le ``mockGenerator``.

La méthode ``generate`` prend trois paramètres :

* le nom de l'interface ou de la classe à bouchonner ;
* le nouvel espace de nom, optionnel ;
* le nouveau nom de la classe, optionnel.

.. code-block:: php

   <?php
   // création d'un bouchon de l'interface \Countable vers \MyMock\Countable
   // on ne change que l'espace de nom
   $this->mockGenerator->generate('\Countable', '\MyMock');

   // création d'un bouchon de la classe abstraite
   // \Vendor\Project\AbstractClass to \MyMock\AClass
   // on change l'espace de nom et le nom de la classe
   $this->mockGenerator->generate('\Vendor\Project\AbstractClass', '\MyMock', 'AClass');

   // création d'un bouchon de la classe \StdClass vers \mock\OneClass
   // on ne change que le nom de la classe
   $this->mockGenerator->generate('\StdClass', null, 'OneClass');

   // on peut maintenant instancier ces mocks
   $vendorAppMock = new \myMock\AClass;
   $countableMock = new \myMock\Countable;
   $stdObject     = new \mock\OneClass;

.. note::
	Si vous n'utilisez que le premier argument et ne changez pas le namespace ou le nom de la classe,
	alors la première solution est équivalente, plus simple à lire et recommandée.

	Vous pouvez accéder au code généré pour la classe par le générateur de mock en appelant
	``$this->mockGenerator->getMockedClassCode()``, pour débuguer par exemple. Cette
	méthode prend les mêmes arguments que la méthode ``generate``.

.. code-block:: php

   <?php
   $countableMock = new \mock\Countable;

   // est équivalent à:

   $this->mockGenerator->generate('\Countable');   // inutile
   $countableMock = new \mock\Countable;

.. note::
	Tout ce qui est décrit ici avec le générateur de mock peut être utilisé avec :ref:`newMockInstance<mock_generate_fast>`

.. _mock_shunt_parent_methods:

Shunter les appels aux méthodes parentes
========================================

.. _mock_shuntParentClassCalls:

shuntParentClassCalls & unShuntParentClassCalls
-----------------------------------------------

Un bouchon hérite directement de la classe à partir de laquelle il a été généré, ses méthodes se comportent donc exactement de la même manière.

Dans certains cas, il peut être utile de shunter les appels aux méthodes parentes afin que leur code ne soit plus exécuté.
Le ``mockGenerator`` met à votre disposition plusieurs méthodes pour y parvenir :

.. code-block:: php

   <?php
   // le bouchon ne fera pas appel à la classe parente
   $this->mockGenerator->shuntParentClassCalls();

   $mock = new \mock\OneClass;

   // le bouchon fera à nouveau appel à la classe parente
   $this->mockGenerator->unshuntParentClassCalls();

Ici, toutes les méthodes du bouchon se comporteront comme si elles n'avaient pas d'implémentation par contre elles conserveront la signature des méthodes originales.

.. note::
	``shuntParentClassCalls`` va *seulement* être appliqué à la prochaine génération de mock. *Mais* si vous créer deux mock de la même classe,
	les deux auront leurs méthodes parente shunté.


.. _mock_shunt:

shunt
-----

Vous pouvez également préciser les méthodes que vous souhaitez shunter :

.. code-block:: php

   <?php
   // le bouchon ne fera pas appel à la classe parente pour la méthode firstMethod…...
   $this->mockGenerator->shunt('firstMethod');
   // ... ni pour la méthode secondMethod
   $this->mockGenerator->shunt('secondMethod');

   $countableMock = new \mock\OneClass;

Une méthode shuntée aura un corps de méthode vide mais comme pour ``shuntParentClassCalls`` la signature de la méthode sera la même que celle bouchonée.

.. _mock_orphan_method:

Rendre une méthode orpheline
============================

Il peut parfois être intéressant de rendre une méthode orpheline, c'est-à-dire, lui donner une signature et une implémentation vide. Cela peut être
particulièrement utile pour générer des bouchons sans avoir à instancier toutes leurs dépendances. Tous les paramètres de la méthode seront également définis
avec comme valeur par défaut null. C'est donc la même chose que :ref:`shunter une méthode<mock_shunt>` mais avec tout les paramètres a null.

.. code-block:: php

   <?php
   class FirstClass {
       protected $dep;

       public function __construct(SecondClass $dep) {
           $this->dep = $dep;
       }
   }

   class SecondClass {
       protected $deps;

       public function __construct(ThirdClass $a, FourthClass $b) {
           $this->deps = array($a, $b);
       }
   }

   $this->mockGenerator->orphanize('__construct');
   $this->mockGenerator->shuntParentClassCalls();

   // Nous pouvons instancier le bouchon sans injecter ses dépendances
   $mock = new \mock\SecondClass();

   $object = new FirstClass($mock);

.. note::
	``orphanize`` va *seulement* être appliqué à la prochaine génération de mock.
