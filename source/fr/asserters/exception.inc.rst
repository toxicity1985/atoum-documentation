.. _exception-anchor:

exception
*********

C'est l'assertion dédiée aux exceptions.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() use($myObject) {
               // ce code lève une exception: throw new \Exception;
               $myObject->doOneThing('wrongParameter');
           }
       )
   ;

.. note::
   La syntaxe utilise les fonctions anonymes (aussi appelées fermetures ou closures), qui sont une fonctionnalité standard de PHP.
   Pour plus de précision, lisez la documentation PHP sur `les fonctions anonymes <http://php.net/functions.anonymous>`_.

Nous pouvons même facilement récupérer la dernière exception via ``$this->exception``.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() use($myObject) {
               // ce code lève une exception: throw new \Exception('erreur', 42);
               $myObject->doOneThing('wrongParameter');
           }
       )->isIdenticalTo($this->exception) // passes
   ;
   
   $this->exception->hasCode(42); // passes
   $this->exception->hasMessage('erreur'); // passes

.. note::
   Avant atoum 3.0.0, si vous avez besoin d'effectuer des assertions, vous aviez besoin d'ajouter ``atoum\test $test`` en argument de la closure. Après la version 3.0.0, vous pouvez simplement utiliser $this à l'intérieur de la closure, afin d'effectuer des assertions.

.. _has-code:

hasCode
=======

``hasCode`` vérifie le code de l'exception.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() use($myObject) {
               // ce code lève une exception: throw new \Exception('erreur', 42);
               $myObject->doOneThing('wrongParameter');
           }
       )
           ->hasCode(42)
   ;

.. _has-default-code:

hasDefaultCode
==============

``hasDefaultCode`` vérifie que le code de l'exception est la valeur par défaut, c'est-à-dire 0.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() use($myObject) {
               // ce code lève une exception: throw new \Exception;
               $myObject->doOneThing('wrongParameter');
           }
       )
           ->hasDefaultCode()
   ;

.. note::
   ``hasDefaultCode`` is equivalent to ``hasCode(0)``.


.. _has-message:

hasMessage
==========

``hasMessage`` vérifie le message de l'exception.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() use($myObject) {
               // ce code lève une exception: throw new \Exception('Message');
               $myObject->doOneThing('wrongParameter');
           }
       )
           ->hasMessage('Message')     // passes
           ->hasMessage('message')     // fails
   ;

.. _has-nested-exception:

hasNestedException
==================

``hasNestedException`` vérifie que l'exception contient une référence vers l'exception précédente. Si le type d'exception est fournie, cela va aussi vérifier la classe de l'exception.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() use($myObject) {
               // ce code lève une exception: throw new \Exception('Message');
               $myObject->doOneThing('wrongParameter');
           }
       )
           ->hasNestedException()      // fails

       ->exception(
           function() use($myObject) {
               try {
                   // ce code lève une exception: throw new \FirstException('Message 1', 42);
                   $myObject->doOneThing('wrongParameter');
               }
               // ... l'exception est attrapée...
               catch(\FirstException $e) {
                   // ... puis relancée, encapsulée dans une seconde exception
                   throw new \SecondException('Message 2', 24, $e);
               }
           }
       )
           ->isInstanceOf('\FirstException')           // fails
           ->isInstanceOf('\SecondException')          // passes

           ->hasNestedException()                      // passes
           ->hasNestedException(new \FirstException)   // passes
           ->hasNestedException(new \SecondException)  // fails
   ;

.. _exception-is-clone-of:

isCloneOf
=========

.. seealso::
   ``isCloneOf`` est une méthode héritée de l'asserter ``object``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`object::isCloneOf <object-is-clone-of>`


.. _exception-is-equal-to:

isEqualTo
=========

.. seealso::
   ``isEqualTo`` est une méthode héritée de l'asserter ``object``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`object::isEqualTo <object-is-equal-to>`


.. _exception-is-identical-to:

isIdenticalTo
=============

.. seealso::
   ``isIdenticalTo`` est une méthode héritée de l'asserter ``object``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`object::isIdenticalTo <object-is-identical-to>`


.. _exception-is-instance-of:

isInstanceOf
============

.. seealso::
   ``isInstanceOf`` est une méthode héritée de l'asserter ``object``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`object::isInstanceOf <object-is-instance-of>`


.. _exception-is-not-equal-to:

isNotEqualTo
============

.. seealso::
   ``isNotEqualTo`` est une méthode héritée de l'asserter ``object``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`object::isNotEqualTo <object-is-not-equal-to>`


.. _exception-is-not-identical-to:

isNotIdenticalTo
================

.. seealso::
   ``isNotIdenticalTo`` est une méthode héritée de l'asserter ``object``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`object::isNotIdenticalTo <object-is-not-identical-to>`


.. _message-anchor:

message
=======

``message`` vous permet de récupérer un asserter de type :ref:`string <string-anchor>` contenant le message de l'exception testée.

.. code-block:: php

   <?php
   $this
       ->exception(
           function() {
               throw new \Exception('My custom message to test');
           }
       )
           ->message
               ->contains('message')
   ;
