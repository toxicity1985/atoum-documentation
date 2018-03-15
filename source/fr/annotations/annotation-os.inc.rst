.. _annotation-os:

Système d'exploitation
**********************

Si vous désirez définir des tests unitaires uniquement pour certains systèmes d'exploitation, ou alors pour qu'ils ne s'exécutent pas sur certains systèmes d'exploitation, vous pouvez utiliser l'annotation `@os`.
Vous pouvez spécifier un ou plusieurs systèmes d'exploitation, ou alors d'éviter un système particulier en le prefixant par "!"
You can define one or several OS, and you can avoid an OS by prefixing it with "!".

.. code-block:: php

   <?php

   namespace vendor\project\tests\units;

   class foo extends \atoum
   {
       /**
        * @os linux
        */
       public function testBar()
       {
           // ...
       }
   }

Ce test ne sera exécuté que si le système d'exploitation courant est Linux.


.. code-block:: php

   <?php

   namespace vendor\project\tests\units;

   class foo extends \atoum
   {
       /**
        * @os !darwin
        */
       public function testBar()
       {
           // ...
       }
   }

Ce test ne sera exécuté que si le système d'exploitation courant n'est pas Darwin


.. note::
   Le système d'exploitation courant est récupéré depuis la constante PHP prédéfinie `__PHP_OS__`.

