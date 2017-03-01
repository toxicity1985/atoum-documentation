
.. _mock-constant:

The mocking of constant
***********************

PHP constant can be declared with ``defined``, but with atoum you can mock it like this:

.. code-block:: php

   <?php
   $this->constant->PHP_VERSION_ID = '606060'; // troll \o/

   $this
       ->given($this->newTestedInstance())
       ->then
           ->variable($this->testedInstance->hello())->isEqualTo(PHP_VERSION_ID)
       ->if($this->constant->PHP_VERSION_ID = uniqid())
       ->then
           ->variable($this->testedInstance->hello())->isEqualTo(PHP_VERSION_ID)
   ;

Warning, due to the nature of constant in PHP, following the :ref:`engine<@engine>` you can meet some issue. Here is an example:

.. code-block:: php

   <?php

   namespace foo {
       class foo {
           public function hello()
           {
               return PHP_VERSION_ID;
           }
       }
   }

   namespace tests\units\foo {
       use atoum;

       /**
        * @engine inline
        */
       class foo extends atoum
       {
           public function testFoo()
           {
               $this
                   ->given($this->newTestedInstance())
                   ->then
                       ->variable($this->testedInstance->hello())->isEqualTo(PHP_VERSION_ID)
                   ->if($this->constant->PHP_VERSION_ID = uniqid())
                   ->then
                       ->variable($this->testedInstance->hello())->isEqualTo(PHP_VERSION_ID)
               ;
           }

           public function testBar()
           {
               $this
                   ->given($this->newTestedInstance())
                   ->if($this->constant->PHP_VERSION_ID = $mockVersionId = uniqid()) // inline engine will fail here
                   ->then
                       ->variable($this->testedInstance->hello())->isEqualTo($mockVersionId)
                   ->if($this->constant->PHP_VERSION_ID = $mockVersionId = uniqid()) // isolate/concurrent engines will fail here
                   ->then
                       ->variable($this->testedInstance->hello())->isEqualTo($mockVersionId)
               ;
           }
       }
   }
