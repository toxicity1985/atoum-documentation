
.. _mock_behaviour_change:

Modify the behaviour of a mock
******************************

Once the mock is created and instantiated, it is often useful to be able to change the behaviour of its methods. To do this,
you must use its controller using one of the following methods:

* $yourMock->getMockController()->yourMethod
* $this->calling($yourMock)->yourMethod

.. code-block:: php

   <?php
   $mockDbClient = new \mock\Database\Client();

   $mockDbClient->getMockController()->connect = function() {};
   // Equivalent to
   $this->calling($mockDbClient)->connect = function() {};

The ``mockController`` allows you to redefine **only public and abstract protected methods** and puts at your disposal several methods:

.. code-block:: php

   <?php
   $mockDbClient = new \mock\Database\Client();

   // Redefine the method connect: it will always return true
   $this->calling($mockDbClient)->connect = true;

   // Redefine the method select: it will execute the given anonymous function
   $this->calling($mockDbClient)->select = function() {
       return array();
   };

   // redefine the method query with arguments
   $result = array();
   $this->calling($mockDbClient)->query = function(Query $query) use($result) {
       switch($query->type) {
           case Query::SELECT:
               return $result;

           default;
               return null;
       }
   };

   // the method connects will throw an exception
   $this->calling($mockDbClient)->connect->throw = new \Database\Client\Exception();

.. note::
	The syntax uses anonymous functions (also called closures), which are a standard feature in PHP.
	Refer to the `PHP manual <http://php.net/functions.anonymous>`__ for more information on the subject.

As you can see, it is possible to use several methods to get the desired behaviour:

* Use a static value that will be returned by the method
* Use a short implementation thanks to anonymous functions of PHP
* Use the ``throw`` keyword to throw an exception

Change mock behaviour on multiple calls
=======================================

You can also specify multiple values based on the order of call:

.. code-block:: php

   <?php
   // default
   $this->calling($mockDbClient)->count = rand(0, 10);
   // equivalent to
   $this->calling($mockDbClient)->count[0] = rand(0, 10);

   // 1st call
   $this->calling($mockDbClient)->count[1] = 13;

   // 3rd call
   $this->calling($mockDbClient)->count[3] = 42;

* The first call will return 13.
* The second will be the default behaviour, it means a random number.
* The third call will return 42.
* All subsequent calls will have the default behaviour, i.e. random numbers.

If you want several methods of the mock have the same behaviour, you can use the `methods<mock_methods>` or `methodsMatching<mock_method_matching>`.




.. _mock_methods:

methods
=======

``methods`` allow you, thanks to the anonymous function passed as an argument, to define what methods the behaviour must be modified:

.. code-block:: php

   <?php
   // if the method has such and such name,
   // we redefine its behaviour
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

   // we redefines the behaviour of all methods
   $this
       ->calling($mock)
           ->methods()
               ->return = null
   ;

   // if the method begins by "get",
   // we redefine its behaviour
   $this
       ->calling($mock)
           ->methods(
               function($method) {
                   return substr($method, 0, 3) == 'get';
               }
           )
               ->return = uniqid()
   ;


In the last example, you should instead use `methodsMatching<mock_method_matching>`.

.. note::
	The syntax uses anonymous functions (also called closures), which are a standard feature in PHP.
	Refer to the `PHP manual <http://php.net/functions.anonymous>`__ for more information on the subject.


.. _mock_method_matching:

methodsMatching
===============

``methodsMatching`` allows you to set the methods where the behaviour must be modified using the regular
expression passed as an argument :

.. code-block:: php

   <?php
   // if the method begins by "is",
   // we redefines its behaviour
   $this
       ->calling($mock)
           ->methodsMatching('/^is/')
               ->return = true
   ;

   // if the method starts by "get" (case insensitive),
   // we redefines its behaviour
   $this
       ->calling($mock)
           ->methodsMatching('/^get/i')
               ->throw = new \exception
   ;

.. note::
	``methodsMatching`` use `preg_match <http://php.net/preg_match>`_ and regular expressions. Refer
	to the `PHP manual <http://php.net/pcre>`__ for more information on the subject.

isFluent && returnThis
======================

Defines a fluent method, so the method return the class.

.. code-block:: php

	<?php
		$foo = new \mock\foo();
		$this->calling($foo)->bar = $foo;

		// is the same as
		$this->calling($foo)->bar->isFluent;
		// or this other one
		$this->calling($foo)->bar->returnThis;

doesNothing && doesSomething
============================

Change the behaviour of the mock with ``doesNothing``, the method will simply return null.

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

		// is the same as
		$this->calling($foo)->bar->doesNothing;
		$this->variable($foo->bar())->isNull;

		// restore the behaviour
		$this->calling($foo)->bar->doesSomething;
		$this->string($foo->bar())->isEqualTo('baz');

Like you see in this example, if for any reason, you want to restore the behaviour of the method, use ``doesSomething``.

.. _mock_special_constructor:

Particular case of the constructor
==================================

To mock class constructor, you need:

* create an instance of \\atoum\\mock\\controller class before you call the constructor of the mock ;
* set via this control the behaviour of the constructor of the mock using an anonymous function ;
* inject the controller during the instantiation of the mock in the `last` argument.

.. code-block:: php

   <?php
   $controller = new \atoum\mock\controller();
   $controller->__construct = function($args)
   {
        // do something with the args
   };

   $mockDbClient = new \mock\Database\Client(DB_HOST, DB_USER, DB_PASS, $controller);

For simple case you can use :ref:`orphanize('__constructor')<mock_orphan_method>` or :ref:`shunt('__constructor')<mock_shunt>`.
