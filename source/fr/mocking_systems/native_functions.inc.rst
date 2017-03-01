
.. _mock-native-function:

The mocking (mock) of native PHP functions
******************************************

atoum allows to easily simulate the behaviours of native PHP functions.

.. code-block:: php

   <?php

   $this
      ->assert('the file exist')
         ->given($this->newTestedInstance())
         ->if($this->function->file_exists = true)
         ->then
         ->object($this->testedInstance->loadConfigFile())
            ->isTestedInstance()
            ->function('file_exists')->wasCalled()->once()

      ->assert('le fichier does not exist')
         ->given($this->newTestedInstance())
         ->if($this->function->file_exists = false )
         ->then
         ->exception(function() { $this->testedInstance->loadConfigFile(); })
   ;

.. important::
	The \\ is not allowed before any functions to simulate because atoum take the resolution mechanism of PHP's namespace.

.. important::
	For the same reason, if a native function was already called before, his mocking will be without any effect.

.. code-block:: php

   <?php

   $this
      ->given($this->newTestedInstance())
      ->exception(function() { $this->testedInstance->loadConfigFile(); }) // the function file_exists and is called before is mocking

      ->if($this->function->file_exists = true ) // the mocking can take the place of the native function file_exists
      ->object($this->testedInstance->loadConfigFile())
         ->isTestedInstance()
   ;

.. note::
	Check the detail about :ref:`isTestedInstance()<object-is-tested-instance>`.
