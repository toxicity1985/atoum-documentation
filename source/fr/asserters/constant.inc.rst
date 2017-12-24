.. _constant-anchor:

constant
********

C'est l'assertion dédiée aux constantes.

.. _constant-isEqualTo:

isEqualTo
=========

``isEqualTo`` vérifie que la constante fournie est égale a la valeur fournie.

.. code-block:: php

   <?php
   namespace
   {
      define('YOLO', 'yolo');
   }

   namespace Foo\test\unit
   {
      class Bar extends \atoum
      {
         public function testWithConstant()
         {
            $this->constant(YOLO)
               ->isEqualTo('yolo');
            $this->string(YOLO)
               ->isEqualTo('yolo');
            }
         }
   }
