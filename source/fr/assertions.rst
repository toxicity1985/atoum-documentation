.. _asserters_collection:

Listes des asserters
#####################

..
.. .. sidebar:: TOC
..
..  .. contents::
..    :depth: 2
..    :local:

atoum possède une série d'asserter et d'assertion relative a ceux-ci. Tous sont listé ici. atoum essaie de vous aider à écrire des tests. Vous rencontrez toujours une syntaxe du genre
``$this->[asserter]($value)->[assertion];``. La plupart des assertions sont chaînable, comme vous pourrez le voir dans le les exemples.

.. note::
	A la fin du chapitre, vous trouverez plusieurs :ref:`trucs & astuces<asserter_tips>` relatif aux assertions et asserters, pensez à le lire!

.. please keep this ordered in an alphabetic way thanks

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
