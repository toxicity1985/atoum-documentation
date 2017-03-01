.. _resource:

resource
********

It's the assertion dedicated to the resources.


.. _resource-isOfType:

isOfType
========

Compare the type of resource with the given type (as string).

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

->is*() will match the type of the stream against a pattern computed from the method name:
	->isFooBar() will try to match a stream with type foo bar, fooBar, foo_bar, ...

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

->$type is an helper providing a :ref:`string asserter<string-anchor>` on the stream type.
