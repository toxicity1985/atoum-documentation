.. _asserters_collection:

Listes des asserters
#####################

..
.. .. sidebar:: TOC
..
..  .. contents::
..    :depth: 2
..    :local:

Afin de permettre d'écrire des tests trés explicites et le moins verbeux possible, atoum dispose d'une série d'asserters donnant accés à des assertions spécifiques au type de variable concernés.

Comme les différents asserters d'atoum sont des spécialisations de plus en plus précises des objets manipulés, les asserters héritent des asserters qu'ils précisent.
Cela permet de conserver les mêmes noms d'assertions entre les asserters, et de garantir un fonctionnement homogène quel que soit l'asserter utilisé

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
    La syntaxe générale asserter/assertion est la suivante :
    ``$this->[asserter]($value)->[assertion];``

.. note::
    La plupart des assertions sont chaînable, comme vous pourrez le voir dans les exemples.

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
