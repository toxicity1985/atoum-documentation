
.. _data-provider:

Data providers
**************

To help you to effectively test your classes, atoum provide you some data providers.

A data provider is a method in class test which generate arguments for test method, arguments that will be used by the method to validate assertions.

If a test method ``testFoo`` takes arguments and no annotation on a data provider is set, atoum will automatically seek the protected ``testFooDataProvider`` method.

However, you can manually set the method name of the data provider through the ``@dataProvider`` annotation applied to the relevant test method, as follows :

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

Obviously, do not forget to define, at the level of the test method, arguments that correspond to those that will be returned by the data provider. If not, atoum will generate an error when running the tests.

The data provider method is a single protected method that returns an array or an iterator containing data :

.. code-block:: php

   <?php
   class calculator extends atoum
   {
       // ...

       // Provides data for testSum().
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

When running the tests, atoum will call test method ``testSum()`` with the arguments ``(1, 1)``, ``(1, 2)``, ``(-1, 1)`` and ``(-1, 2)`` returned by the method ``sumDataProvider()``.

.. warning::
   The insulation of the tests will not be used in this context, which means that each successive call to the method ``testSum()`` will be realized in the same PHP process.

.. _data-provider-closure:

Data provider as closure
========================

You can also use a closure to define a data provider instead of an annotation. In your method :ref:`beforeTestMethod<initialization_method>`, you can use this example:

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

Data provider injected in test method
=====================================

There is also, an injection of mock in the test method parameters. So take a simple example:

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

You can write this instead:

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

In this case, no need for data provider. But, if you want to customize the mock you will require it or use :ref:`beforeTestMethod<initialization_method>`.

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
           // orphanize the controller for the next mock generated, here $iterator
           $this->mockGenerator->orphanize('__construct');
       }
   }
