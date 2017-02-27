

.. _@engine:

Execution engine
****************

Several execution engines to run the tests (at the class or method level) are available. These are configurable via the ``@engine`` annotation. By default, the different tests run in parallel in PHP sub-processes, this is the ``concurrent`` mode.

There are currently three execution modes: :

* *inline*: tests run in the same process, this is the same behaviour as PHPUnit. Although this mode is very fast, there's no insulation of the tests.
* *isolate*: tests run sequentially in a subprocess of PHP. This form of execution is quite slow.
* *concurrent*: the default mode, the tests run in parallel, in PHP sub-processes. 

.. important::
  If you use xdebug to debug your tests (and not only for code coverage), the only execution engine available is `concurrent`.

Here's an example :

.. code-block:: php

  <?php
  
  /**
   * @engine concurrent
   */
  class Foo extends \atoum
  {
  	public function testBarWithBaz()
  	{
  		sleep(1);
  		$this->newTestedInstance;
  		$baz = new \Baz();
  		$this->object($this->testedInstance->setBaz($baz))
  			->isIdenticalTo($this->testedInstance);
  			
  		$this->string($this->testedInstance->bar())
  			->isIdenticalTo('baz');
  	}
  	
  	public function testBarWithoutBaz()
  	{
  		sleep(1);
  		$this->newTestedInstance;
  		$this->string($this->testedInstance->bar())
  			->isIdenticalTo('foo');
  	}
  }

In ``concurrent`` mode :

.. code-block:: shell

  => Test duration: 2.01 seconds.
  => Memory usage: 0.50 Mb.
  > Total test duration: 2.01 seconds.
  > Total test memory usage: 0.50 Mb.
  > Running duration: 1.08 seconds.


In ``inline`` mode :

.. code-block:: shell

  => Test duration: 2.01 seconds.
  => Memory usage: 0.25 Mb.
  > Total test duration: 2.01 seconds.
  > Total test memory usage: 0.25 Mb.
  > Running duration: 2.01 seconds.


In ``isolate`` mode :

.. code-block:: shell

  => Test duration: 2.00 seconds.
  => Memory usage: 0.50 Mb.
  > Total test duration: 2.00 seconds.
  > Total test memory usage: 0.50 Mb.
  > Running duration: 2.10 seconds.

