.. _asserter_tips:

Asserter & assertion tips
*************************

Several tips & trick are available for the assertion. Knowing them can simplify your life ;)

The first one is that all assertion are fluent. So you can chain them, just look at the previous example.

You should also know that all assertions can be written with or without parenthesis. So ``$this->integer(0)->isZero()`` is the same as ``$this->integer(0)->isZero``.

.. _asserter_tips-alias:

Alias
=====

TODO

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

.. _asserter-custom:

Custom asserter
===============

TODO

.. https://github.com/jubianchi/jubianchi.github.io/blob/371b9da3232cfa5b8ad5b7b9dc8860ff39fb663b/atoum-alias.md

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



.. _asserter_tips-short:

Short syntax
============

TODO

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





