.. _asserters_collection:

Listes des asserters
#####################

..
.. .. sidebar:: TOC
..
..  .. contents::
..    :depth: 2
..    :local:

Pour écrire des tests plus explicites et moins verbeux, atoum fourni plusieurs asserter qui donnent accès a des assertions spécifiques associées aux valeurs testés.

atoum possède différents asserters spécialisés permettant de manipuler différents éléments, les assertes hérite des autres asserters qu'ils spécialisent.
Ceci permettant d'aider à garder une consistance entre les différents asserters et force à utiliser les nom d'assertion.

Voici l'arbre d'héritage des asserters :

.. code-block:: shell

    -- asserter (abstract)
        |-- error
        |-- mock
        |-- stream
        `-- variable
            |-- array
            |    `-- castToArray
            |-- boolean
            |-- class
            |    `-- testedClass
            |-- integer
            |   |-- float
            |   `-- sizeOf
            |-- object
            |   |-- dateInterval
            |   |-- dateTime
            |   |   `-- mysqlDateTime
            |   `-- exception
            |-- resource
            `-- string
                |-- castToString
                |-- hash
                |-- output
                `-- utf8String


.. note::
    La syntaxe général des asserter/assertion est :
    ``$this->[asserter]($value)->[assertion];``

.. note::
    La plupart des assertions sont fluent, comme vous le verrez ci-dessous.

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
.. include:: asserters/extension.inc.rst
.. include:: asserters/float.inc.rst
.. include:: asserters/hash.inc.rst
.. include:: asserters/integer.inc.rst
.. include:: asserters/mock.inc.rst
.. include:: asserters/mysqlDateTime.inc.rst
.. include:: asserters/object.inc.rst
.. include:: asserters/output.inc.rst
.. include:: asserters/resource.inc.rst
.. include:: asserters/sizeOf.inc.rst
.. include:: asserters/stream.inc.rst
.. include:: asserters/string.inc.rst
.. include:: asserters/utf8String.inc.rst
.. include:: asserters/variable.inc.rst



.. include:: asserters/ztips.inc.rst
