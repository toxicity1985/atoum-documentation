.. _asserter_tips:

Asserter & assertion trucs et astuces
*************************************

Plusieurs trucs et astuces sont disponibles pour les assertions. Les connaître peuvent simplifier votre vie  ;)

Le premier est que chaque assertion est fluent (chaînable). Donc vous pouvez les enchaîner, il suffit de regarder les exemples précédents.

Vous devez également savoir que toutes les assertions sans paramètres peuvent être écrites avec ou sans parenthèses.
Donc ``$this->integer(0)->isZero()`` est la même chose que ``$this->integer(0)->isZero``.

.. _asserter_tips-alias:

Alias
=====

Parfois, vous voulez utiliser quelque chose qui reflètent votre vocabulaire ou votre domaine. atoum fournis un mécanisme simple, les alias.
En voici un exemple :

.. code-block:: php

	<?php
	namespace tests\units;

	use mageekguy\atoum;

	class stdClass extends atoum\test
	{
	    public function __construct(adapter $adapter = null, annotations\extractor $annotationExtractor = null, asserter\generator $asserterGenerator = null, test\assertion\manager $assertionManager = null, \closure $reflectionClassFactory = null)
	    {
	        parent::__construct($adapter, $annotationExtractor, $asserterGenerator, $assertionManager, $reflectionClassFactory);

	        $this
	            ->from('string')->use('isEqualTo')->as('equals')
	        ;
	    }

	    public function testFoo()
	    {
	        $this
	            ->string($u = uniqid())->equals($u)
	        ;
	    }
	}

Dans cet exemple, nous créons un alias pour faire un nouvel asserter ``equal```qui agira de la même manière que 
``isEqualTo``. Vous pouvez utiliser :ref:`beforeTestMethod<initialization_method>` à la place du constructeur. Afin de partager ces alias entre les différents tests, le mieux est de
créer une classe de base pour vos tests à l'intérieur de votre projet que vous pourrez étendre à la place ``\atoum\test``.

.. _asserter-custom:

Asserter personnalisé
=====================

Maintenant que nous avons vu alias, nous pouvons aller plus loin en créant un asserter personnalisé. Voici un exemple d’un asserter pour carte de crédit.

.. code-block:: php

	<?php
	namespace tests\units;
	use mageekguy\atoum;

	class creditcard extends atoum\asserters\string
	{
	    public function isValid($failMessage = null)
	    {
	        return $this->match('/(?:\d{4}){4}/', $failMessage ?: $this->_('%s is not a valid credit card number', $this));
	    }
	}

	class stdClass extends atoum\test
	{
	    public function __construct(adapter $adapter = null, annotations\extractor $annotationExtractor = null, asserter\generator $asserterGenerator = null, test\assertion\manager $assertionManager = null, \closure $reflectionClassFactory = null)
	    {
	        parent::__construct($adapter, $annotationExtractor, $asserterGenerator, $assertionManager, $reflectionClassFactory);

	        $this->getAsserterGenerator()->addNamespace('tests\units');
	    }

	    public function testFoo()
	    {
	        $this
	            ->creditcard('4444555566660000')->isValid()
	        ;
	    }
	}

Tout comme pour un alias, il est conseillé de créer une classe de base pour vos tests et déclarer l'asserter personnalisé à cet endroit.

.. _asserter_tips-short:

Syntaxe courte
==============

Avec un :ref:`alias<asserter_tips-alias>` vous pouvez définir plusieurs choses intéressantes. Afin de vous aider dans la rédaction de vos tests,  plusieurs alias sont disponibles nativement.

* **==** est la même chose que l'asserter :ref:`isEqualTo<variable-is-equal-to>`
* **===** est la même chose que l'asserter :ref:`isIdenticalTo<variable-is-identical-to>`
* **!=** est la même chose que l'asserter :ref:`isNotEqualTo<variable-is-not-equal-to>`
* **!==** est la même chose que l'asserter :ref:`isNotIdenticalTo<variable-is-not-identical-to>`
* **<** est équivalent à :ref:`isLessThan<integer-is-less-than>`
* **<=** est la même chose que l'asserter :ref:`isLessThanOrEqualTo<integer-is-less-than-or-equal-to>`
* **>** est la même chose que l'asserter :ref:`isGreaterThan<integer-is-greater-than>`
* **>=** est la même chose que l'asserter :ref:`isGreaterThanOrEqualTo<integer-is-greater-than-or-equal-to>`

.. code-block:: php

	<?php
	namespace tests\units;

	use atoum;

	class stdClass extends atoum
	{
	    public function testFoo()
	    {
	        $this
	            ->variable('foo')->{'=='}('foo')
	            ->variable('foo')->{'foo'} // équivalent à la ligne précédente
	            ->variable('foo')->{'!='}('bar')

	            ->object($this->newInstance)->{'=='}($this->newInstance)
	            ->object($this->newInstance)->{'!='}(new \exception)
	            ->object($this->newTestedInstance)->{'==='}($this->testedInstance)
	            ->object($this->newTestedInstance)->{'!=='}($this->newTestedInstance)

	            ->integer(rand(0, 10))->{'<'}(11)
	            ->integer(rand(0, 10))->{'<='}(10)
	            ->integer(rand(0, 10))->{'>'}(-1)
	            ->integer(rand(0, 10))->{'>='}(0)
	        ;
	    }
	}
