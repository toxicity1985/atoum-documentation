.. _function-anchor:

function
********

C'est l'asserter dédié aux :ref:`fonctions natives <mock-native-function>` qui sont mockée.

.. _function-wasCalled:

wasCalled
=========

``wasCalled`` vérifie que la fonction mockée a été appelée.

.. _function-wasCalledWithArguments:

wasCalledWithArguments
======================

``wasCalledWithArguments`` permet de vérifier les arguments  utilisé avec l'appel de la fonction.

.. _function-wasCalledWithIdenticalArguments:

wasCalledWithIdenticalArguments
===============================

``wasCalledWithIdenticalArguments`` permet de vérifier tous les arguments utilisé avec l'appel de la fonction.

.. _function-wasCalledWithoutAnyArgument:

wasCalledWithoutAnyArgument
===========================

``wasCalledWithoutAnyArgument`` vérifie que l'appel a la fonction a été effectué sans aucun argument.


.. _function-count_all:

Compter les appels
==================

Si vous voulez vous pouvez effectuer une assertion supplémentaire en comptant le nombre d'appel à la fonction.

.. code-block:: php

   <?php
   $this->function->error_log = true;

   $this
      ->if($this->newTestedInstance())
      ->and($this->testedInstance->methodWithAnErrorLog($notExcepted = uniqid()))
      ->then
          ->function('error_log')
              ->wasCalledWithArguments('Value ' . $notExcepted . ' is not excepted here')
                  ->once();

Ici, nous vérifions que notre fonction a été appelée une seule fois, avec les arguments fournis.

.. _function-after:

after
`````

``after`` vérifie que la fonction a été appelée après la méthode passée en paramètre.


.. seealso::
   ``after`` a le même comportement que celui existant sur l'asserter des ``mock``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`mock::after <mock-after>`

.. _function-at-least-once:

atLeastOnce
```````````

``atLeastOnce`` vérifie que la fonction a été appelée au moins une fois.

.. seealso::
   ``atLeastOnce`` a le même comportement que celui de l'asserter des ``mock``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`mock::atLeastOnce <at-least-once>`

.. _function-before:

before
``````

``after`` vérifie que la fonction a été appelée avant la méthode passée en paramètre.

.. seealso::
   ``before`` is the same as the one on the ``mock`` asserter.
   For more information, refer to the documentation of :ref:`mock::before <mock-before>`

.. _function-exactly-anchor:

exactly
```````

``exactly`` check that the mocked function has been called a specific number of times.

.. seealso::
   ``exactly`` is the same as the one on the ``mock`` asserter.
   For more information, refer to the documentation of :ref:`mock::exactly <exactly-anchor>`

.. _function-never-anchor:

never
`````

``never`` check that the mocked function has never been called.

.. seealso::
   ``never`` is the same as the one on the ``mock`` asserter.
   For more information, refer to the documentation of :ref:`mock::never <never-anchor>`

.. _function-once-twice-thrice:

once/twice/thrice
`````````````````
This asserters check that the mocked function has been called exactly:

* une fois (once)
* deux fois (twice)
* trois fois (thrice)

.. seealso::
   ``once`` is the same as the one on the ``mock`` asserter.
   For more information, refer to the documentation of :ref:`mock::once/twice/thrice <once-twice-thrice>`
