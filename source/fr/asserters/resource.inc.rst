.. _resource:

resource
********

C'est l'assertion dédié au ´ressource <http://php.net/language.types.resource>´_.


.. _resource-isOfType:

isOfType
========

Cette méthode permet de comparer le type de ressource avec le type de la valeur fournie en paramètre. Dans l'exemple suivant, on vérifie que le paramètre est un stream.

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
