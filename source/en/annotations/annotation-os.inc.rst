.. _annotation-os:

Operating system
****************

If you want to define tests scenario for specific OS, or to be avoided on specific OS, you can use the tag `@os`.
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

The test will only be executed if the current OS is linux

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

The test will only be executed on all other OS than Darwin

.. note::
   OS value for the current system is checked in the PHP predefined constant `__PHP_OS__`.

