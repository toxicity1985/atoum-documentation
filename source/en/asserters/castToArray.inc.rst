.. _cast-to-array:

castToArray
************

It's the assertion dedicated to tests on the cast of objects to arrays.

.. code-block:: php

   <?php
   class AtoumVersions {
       private $versions = ['1.0', '2.0', '2.1'];

       public function __toArray() {
           return $this->versions;
       }
   }

   $this
       ->castToArray(new AtoumVersions())
           ->contains('1.0')
   ;


.. hint::
   ``castToArray`` asserter return an instance of ``array`` asserter.
   You can use all assertions from :ref:`array <array-anchor>` asserter
