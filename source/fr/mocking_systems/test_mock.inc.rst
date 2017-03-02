
.. _mock_test_mock:

Tester un bouchon
*********

atoum vous permet de vérifier qu'un bouchon a été utilisé correctement.

.. code-block:: php

   <?php
   $mockDbClient = new \mock\Database\Client();
   $mockDbClient->getMockController()->connect = function() {};
   $mockDbClient->getMockController()->query   = array();

   $bankAccount = new \Vendor\Project\Bank\Account();
   $this
       // utilisation du bouchon via un autre objet
       ->array($bankAccount->getOperations($mockDbClient))
           ->isEmpty()

       // test du bouchon
       ->mock($mockDbClient)
           ->call('query')
               ->once() // vérifie que la méthode query
                               // n'a été appelé qu'une seule fois
   ;

.. note::
	Reportez-vous à la documentation sur l'assertion :ref:`mock-asserter` pour obtenir plus d'informations sur les tests des bouchons.
