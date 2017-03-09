.. _resource:

resource
********

It's the assertion dedicated to the ´resources <http://php.net/language.types.resource>´_.


.. _resource-isOfType:

isOfType
========

This method compare the type of resource with the type of the given value provided by the argument. In the following example, we checks that the given value is a stream.

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
