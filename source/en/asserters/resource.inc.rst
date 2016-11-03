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

phpResource:: is*() will match the type of the stream against a pattern computed from the method name: ->isFooBar() will try to match a stream with type foo bar, fooBar, foo_bar, ...

.. _resource-type:

type
====


.. code-block:: php

	$this
	    ->resource($variable)
	        ->type
				->isEqualTo('stream')
	;



    phpResource:: is*() will match the type of the stream against a pattern computed from the method name: ->isFooBar() will try to match a stream with type foo bar, fooBar, foo_bar, ...
    phpResource::$type is an helper providing a string asserter on the stream type so that the user can do things like ->type->matches('/foo.*bar/')


Yup, ->type fallbacks to the string asserters.