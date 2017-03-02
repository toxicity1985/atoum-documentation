
.. _mock-constant:

Les bouchons de constantes
**************************

Les constantes PHP peuvent être déclarée avec ``defined``, cependant avec atoum vous pouvez les bouchonner de cette manière :

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

Attention, due à la nature des constantes en PHP, suivant :ref:`l'engine<@engine>` utiliser vous pouvez différent problème. En voici un exemple :

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
