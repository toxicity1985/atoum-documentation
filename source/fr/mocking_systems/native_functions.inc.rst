
.. _mock-native-function:

Le bouchonnage (mock) des fonctions natives de PHP
**************************************************

atoum permet de très facilement simuler le comportement des fonctions natives de PHP.

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
	On ne peut pas mettre de \\ devant les fonctions à simuler, car atoum s’appuie sur le mécanisme de résolution des espaces de nom de PHP.

.. important::
	Pour la même raison, si une fonction native a déjà été appelée, son bouchonnage sera sans effet.

.. code-block:: php

   <?php

   $this
      ->given($this->newTestedInstance())
      ->exception(function() { $this->testedInstance->loadConfigFile(); }) //la fonction file_exists est appelée avant son bouchonnage

      ->if($this->function->file_exists = true ) // le bouchonnage ne pourra pas prendre la place de la fonction native file_exists
      ->object($this->testedInstance->loadConfigFile())
         ->isTestedInstance()
   ;

.. note::
	Plus d'information via :ref:`isTestedInstance()<object-is-tested-instance>`.
