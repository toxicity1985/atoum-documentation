.. _output-anchor:

output
******

C'est l'assertion dédiée aux tests sur les sorties, c'est-à-dire tout ce qui est censé être affiché à l'écran.

.. code-block:: php

   <?php
   $this
       ->output(
           function() {
               echo 'Hello world';
           }
       )
   ;

.. note::
   La syntaxe utilise les fonctions anonymes (aussi appelées fermetures ou closures) introduites en PHP 5.3.
   Pour plus de précision, lisez la documentation PHP sur `les fonctions anonymes <http://php.net/functions.anonymous>`_.


.. _output-contains:

contains
========

.. seealso::
   ``contains`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::contains <string-contains>`


.. _output-has-length:

hasLength
=========

.. seealso::
   ``hasLength`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::hasLength <string-has-length>`


.. _output-has-length-greater-than:

hasLengthGreaterThan
====================

.. seealso::
   ``hasLengthGreaterThan`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::hasLengthGreaterThan <string-has-length-greater-than>`


.. _output-has-length-less-than:

hasLengthLessThan
=================

.. seealso::
   ``hasLengthLessThan`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::hasLengthLessThan <string-has-length-less-than>`


.. _output-is-empty:

isEmpty
=======

.. seealso::
   ``isEmpty`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::isEmpty <string-is-empty>`


.. _output-is-equal-to:

isEqualTo
=========

.. seealso::
   ``isEqualTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isEqualTo <variable-is-equal-to>`


.. _output-is-equal-to-contents-of-file:

isEqualToContentsOfFile
=======================

.. seealso::
   ``isEqualToContentsOfFile`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::isEqualToContentsOfFile <string-is-equal-to-contents-of-file>`


.. _output-is-identical-to:

isIdenticalTo
=============

.. seealso::
   ``isIdenticalTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isIdenticalTo <variable-is-identical-to>`


.. _output-is-not-empty:

isNotEmpty
==========

.. seealso::
   ``isNotEmpty`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::isNotEmpty <string-is-not-empty>`


.. _output-is-not-equal-to:

isNotEqualTo
============

.. seealso::
   ``isNotEqualTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isNotEqualTo <variable-is-not-equal-to>`


.. _output-is-not-identical-to:

isNotIdenticalTo
================

.. seealso::
   ``isNotIdenticalTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isNotIdenticalTo <variable-is-not-identical-to>`


.. _output-matches:

matches
=======

.. seealso::
   ``matches`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::matches <string-matches>`


.. _output-not-contains:

notContains
===========

.. seealso::
   ``notContains`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::notContains <string-not-contains>`
