
There are several ways to write unit test with atoum, one of them is to use keywords like ``given``, ``if``, ``and`` and even ``then``, ``when``  or ``assert`` so you can structure your tests to make them more readable.

.. _given-if-and-then:

``given``, ``if``, ``and`` and ``then``
***************************************

You can use these keywords very intuitively:

.. code-block:: php

   <?php
   $this
       ->given($computer = new computer())
       ->if($computer->prepare())
       ->and(
           $computer->setFirstOperand(2),
           $computer->setSecondOperand(2)
       )
       ->then
           ->object($computer->add())
               ->isIdenticalTo($computer)
           ->integer($computer->getResult())
               ->isEqualTo(4)
   ;

It's important to note that these keywords don't have any another purpose than presenting the test in a more readable format. They don't serve any technical purpose. The only goal is to help the reader, human or more specifically developer, to quickly understand what's happening in the test.

Thus, ``given``, ``if`` and ``and`` specify the prerequisite assertions that follow the keyword ``then`` to pass.

However, there are no rules or grammar that dictate the order ot syntax of these keywords in atoum.

As a result, the developer should use the keywords wisely in order to make the test as readable as possible. If used incorrectly you could end up with tests like the following :

.. code-block:: php

   <?php
   $this
       ->and($computer = new computer())
       ->if($computer->setFirstOperand(2))
       ->then
       ->given($computer->setSecondOperand(2))
           ->object($computer->add())
               ->isIdenticalTo($computer)
           ->integer($computer->getResult())
               ->isEqualTo(4)
   ;

For the same reason, the use of ``then`` is also optional.

Notice that you can write the exact same test without using any of the previous keywords:

.. code-block:: php

   <?php
   $computer = new computer();
   $computer->setFirstOperand(2);
   $computer->setSecondOperand(2);

   $this
       ->object($computer->add())
           ->isIdenticalTo($computer)
       ->integer($computer->getResult())
           ->isEqualTo(4)
   ;

The test will not be slower or faster to run and there is no advantage to use one notation or another, the important thing is to choose one format and stick to it. This facilitates maintenance of the tests (the problem is exactly the same as coding conventions).

.. _when:

when
****

In addition to ``given``, ``if``, ``and`` and ``then``, there are also other keywords.

One of them is ``when``. It has a specific feature introduced to work around the fact that it is illegal to write the following PHP code :

.. code-block:: php

   <?php # ignore
   $this
       ->if($array = array(uniqid()))
       ->and(unset($array[0]))
       ->then
           ->sizeOf($array)
               ->isZero()
   ;

In this case the language will generate a fatal error: ``Parse error: syntax error, unexpected 'unset' (T_UNSET), expecting ')'``

It is impossible to use ``unset()`` as an argument of a function.

To resolve this problem, the keyword ``when`` is able to interpret the possible anonymous function that is passed as an argument, allowing us to write the previous test in the following way:

.. code-block:: php

   <?php
   $this
       ->if($array = array(uniqid()))
       ->when(
           function() use ($array) {
               unset($array[0]);
           }
       )
       ->then
         ->sizeOf($array)
           ->isZero()
   ;

Of course, if ``when`` doesn't receive an anonymous function as an argument, it behaves exactly as ``given``, ``if``, ``and`` and ``then``, namely that it does absolutely nothing functionally speaking.
