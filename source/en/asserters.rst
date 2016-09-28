.. _asserters_collection:

Asserters collection
####################

..
.. .. sidebar:: TOC
..
..  .. contents::
..    :depth: 2
..    :local:

In atoum we have several asserters and related assertions. All are listed here. atoum tries to help you to write test. So you have always a syntax like this
``$this->[asserter]($value)->[assertion];``. Most of the assertions are fluent, like you will see in the the given examples.

.. note::
	At the end of this chapter you will find several :ref:`tips & tricks<asserter_tips>` related to assertion and asserter, don't forget to read it!

.. please keep this ordered in an alphabetic wayi thanks

.. include:: asserters/afterDestructionOf.inc.rst
.. include:: asserters/array.inc.rst
.. include:: asserters/boolean.inc.rst
.. include:: asserters/castToString.inc.rst
.. include:: asserters/class.inc.rst
.. include:: asserters/dateInterval.inc.rst
.. include:: asserters/dateTime.inc.rst
.. include:: asserters/error.inc.rst
.. include:: asserters/exception.inc.rst
.. include:: asserters/float.inc.rst
.. include:: asserters/hash.inc.rst
.. include:: asserters/integer.inc.rst
.. include:: asserters/mock.inc.rst
.. include:: asserters/mysqlDateTime.inc.rst
.. include:: asserters/object.inc.rst
.. include:: asserters/output.inc.rst
.. include:: asserters/sizeOf.inc.rst
.. include:: asserters/stream.inc.rst
.. include:: asserters/string.inc.rst
.. include:: asserters/utf8String.inc.rst
.. include:: asserters/variable.inc.rst



.. include:: asserters/ztips.inc.rst
