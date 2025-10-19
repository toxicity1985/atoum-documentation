.. _output-anchor:

output
******

It's the assertion dedicated to tests on outputs, so everything witch supposed to be displayed on the screen.

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
   The syntax uses anonymous functions (also called closures), which are a standard feature in PHP.
   For more details, read the PHP's documentation on `anonymous functions <http://php.net/functions.anonymous>`_.


.. _output-contains:

contains
========

.. seealso::
   ``contains`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::contains <string-contains>`


.. _output-has-length:

hasLength
=========

.. seealso::
   ``hasLength`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::hasLength <string-has-length>`


.. _output-has-length-greater-than:

hasLengthGreaterThan
====================

.. seealso::
   ``hasLengthGreaterThan`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::hasLengthGreaterThan <string-has-length-greater-than>`


.. _output-has-length-less-than:

hasLengthLessThan
=================

.. seealso::
   ``hasLengthLessThan`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::hasLengthLessThan <string-has-length-less-than>`


.. _output-is-empty:

isEmpty
=======

.. seealso::
   ``isEmpty`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::isEmpty <string-is-empty>`


.. _output-is-equal-to:

isEqualTo
=========

.. seealso::
   ``isEqualTo`` is a method inherited from the ``variable`` asserter.
   For more information, refer to the documentation of :ref:`variable::isEqualTo <variable-is-equal-to>`


.. _output-is-equal-to-contents-of-file:

isEqualToContentsOfFile
=======================

.. seealso::
   ``isEqualToContentsOfFile`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::isEqualToContentsOfFile <string-is-equal-to-contents-of-file>`


.. _output-is-identical-to:

isIdenticalTo
=============

.. seealso::
   ``isIdenticalTo`` is a method inherited from the ``variable`` asserter.
   For more information, refer to the documentation of :ref:`variable::isIdenticalTo <variable-is-identical-to>`


.. _output-is-not-empty:

isNotEmpty
==========

.. seealso::
   ``isNotEmpty`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::isNotEmpty <string-is-not-empty>`


.. _output-is-not-equal-to:

isNotEqualTo
============

.. seealso::
   ``isNotEqualTo`` is a method inherited from the ``variable`` asserter.
   For more information, refer to the documentation of :ref:`variable::isNotEqualTo <variable-is-not-equal-to>`


.. _output-is-not-identical-to:

isNotIdenticalTo
================

.. seealso::
   ``isNotIdenticalTo`` is a method inherited from the ``variable`` asserter.
   For more information, refer to the documentation of :ref:`variable::isNotIdenticalTo <variable-is-not-identical-to>`


.. _output-matches:

matches
=======

.. seealso::
   ``matches`` is a method inherited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::match <string-matches>`


.. _output-not-contains:

notContains
===========

.. seealso::
   ``notContains`` is a method herited from the ``string`` asserter.
   For more information, refer to the documentation of :ref:`string::notContains <string-not-contains>`
