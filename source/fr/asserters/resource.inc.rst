.. _resource:

resource
********

C'est l'assertion dédiée aux ressources.


.. _resource-isOfType:

isOfType
========

Comparer le type de ressource avec le type de donnée fournie (comme une chaîne de caractère).

.. code-block:: php

	$this
	    ->resource($variable)
	        ->isOfType('stream')
	;

.. _resource-isStream:

isStream
========

.. code-block:: php

	$this
	    ->resource($variable)
	        ->isStream()
	;

->is*() va faire correspondre le type du flux au nom d'une méthode :
	->isFooBar() va essayer de trouver un flux correspondant à foo bar, fooBar, foo_bar...

.. _resource-type:

type
====

.. code-block:: php

	$this
	    ->resource($variable)
	        ->type
				->isEqualTo('stream')
				->matches('/foo.*bar/')
	;

->$type est un helper fournissant :ref:`l'assertion des string<string-anchor>` sur le type de stream.
