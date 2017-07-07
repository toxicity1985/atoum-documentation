.. _cast-to-array:

castToArray
************

C'est l'assertion dédiée aux tests sur le transtypage d'objets en tableaux.

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
   L'asserter ``castToArray`` retourne une instance de l'assertion ``array``.
   Vous pouvez donc utiliser toutes les méthodes de l'assertion :ref:`array <array-anchor>`
