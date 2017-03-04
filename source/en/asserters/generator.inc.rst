.. _generator-anchor:

generator
*********

It's the assertion dedicated to tests on `generators <http://php.net/manual/en/language.generators.overview.php>`_.

The generator asserter extends the iterator asserter, so you can use any assertion from the iterator asserter.

Exemple:

.. code-block:: php

   <?php
   $generator = function() {
       for ($i=0; $i<3; $i++) {
           yield ($i+1);
       }
   };
   $this
       ->generator($generator())
           ->size->isEqualTo(3)
   ;


.. _generator-yields:

yields
======

``yields`` is used to ease the test on values yielded by the generator.
Each time you will call ``->yields`` the next value of the generator will be retrived.
You will be able to use any other asserter on this value (for example ``class``, ``string`` or ``variable``).

Example:

.. code-block:: php

   <?php
   $generator = function() {
       for ($i=0; $i<3; $i++) {
           yield ($i+1);
       }
   };
   $this
       ->generator($generator())
           ->yields->variable->isEqualTo(1)
           ->yields->variable->isEqualTo(2)
           ->yields->variable->isEqualTo(3)
           ->yields->variable->isNull()
   ;


.. _generator-returns:

returns
=======

This assertion will only work on PHP >= 7.0.
Since this version, generators can return a value that can retrived via a call to the ``->getReturn(()`` method.
When you call ``->returns`` on the generator asserter, atoum will retrive the value from a call on the ``->getReturn(()`` method on the asserter.
Then you will be able to use any other asserter on this value just like the ``yields`` assertion.

Example:

.. code-block:: php

   <?php
   $generator = function() {
       for ($i=0; $i<3; $i++) {
           yield ($i+1);
       }
       return 42;
   };
   $this
       ->generator($generator())
           ->yields->variable->isEqualTo(1)
           ->yields->variable->isEqualTo(2)
           ->yields->variable->isEqualTo(3)
           ->yields->variable->isNull()
           ->returns->variable->isEqualTo(42)
   ;


History
=======

+-----------+---------------------------+
| Version   | Changes                   |
+===========+===========================+
| `v3.0.0`_ | Generator asserter added. |
+-----------+---------------------------+

.. _v3.0.0: https://github.com/atoum/atoum/blob/master/CHANGELOG.md#300---2017-02-22
