.. _cast-to-string:

castToString
************

C'est l'assertion dédiée aux tests sur le transtypage d'objets en chaîne de caractères.

.. code-block:: php

   <?php
   class AtoumVersion {
       private $version = '1.0';

       public function __toString() {
           return 'atoum v' . $this->version;
       }
   }

   $this
       ->castToString(new AtoumVersion())
           ->isEqualTo('atoum v1.0')
   ;

.. _cast-to-string-contains:

contains
========

.. seealso::
   ``contains`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::contains <string-contains>`


.. _cast-to-string-not-contains:

notContains
===========

.. seealso::
   ``notContains`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::notContains <string-not-contains>`


.. _cast-to-string-has-length:

hasLength
=========

.. seealso::
   ``hasLength`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::hasLength <string-has-length>`


.. _cast-to-string-has-length-greater-than:

hasLengthGreaterThan
====================

.. seealso::
   ``hasLengthGreaterThan`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::hasLengthGreaterThan <string-has-length-greater-than>`


.. _cast-to-string-has-length-less-than:

hasLengthLessThan
=================

.. seealso::
   ``hasLengthLessThan`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::hasLengthLessThan <string-has-length-less-than>`


.. _cast-to-string-is-empty:

isEmpty
=======

.. seealso::
   ``isEmpty`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::isEmpty <string-is-empty>`


.. _cast-to-string-is-equal-to:

isEqualTo
=========

.. seealso::
   ``isEqualTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isEqualTo <variable-is-equal-to>`


.. _cast-to-string-is-equal-to-contents-of-file:

isEqualToContentsOfFile
=======================

.. seealso::
   ``isEqualToContentsOfFile`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::isEqualToContentsOfFile <string-is-equal-to-contents-of-file>`


.. _cast-to-string-is-identical-to:

isIdenticalTo
=============

.. seealso::
   ``isIdenticalTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isIdenticalTo <variable-is-identical-to>`


.. _cast-to-string-is-not-empty:

isNotEmpty
==========

.. seealso::
   ``isNotEmpty`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::isNotEmpty <string-is-not-empty>`


.. _cast-to-string-is-not-equal-to:

isNotEqualTo
============

.. seealso::
   ``isNotEqualTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isNotEqualTo <variable-is-not-equal-to>`


.. _cast-to-string-is-not-identical-to:

isNotIdenticalTo
================

.. seealso::
   ``isNotIdenticalTo`` est une méthode héritée de l'asserter ``variable``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`variable::isNotIdenticalTo <variable-is-not-identical-to>`


.. _cast-to-string-matches:

matches
=======

.. seealso::
   ``matches`` est une méthode héritée de l'asserter ``string``.
   Pour plus d'informations, reportez-vous à la documentation de :ref:`string::matches <string-matches>`
