
.. _mock_test_mock:

Test mock
*********

atoum lets you verify that a mock was used properly.

.. code-block:: php

   <?php
   $mockDbClient = new \mock\Database\Client();
   $mockDbClient->getMockController()->connect = function() {};
   $mockDbClient->getMockController()->query   = array();

   $bankAccount = new \Vendor\Project\Bank\Account();
   $this
       // use of the mock via another object
       ->array($bankAccount->getOperations($mockDbClient))
           ->isEmpty()

       // test of the mock
       ->mock($mockDbClient)
           ->call('query')
               ->once() // check that the query method
                               // has been called only once
   ;

.. note::
	Refer to the documentation on the :ref:`mock-asserter` for more information on testing mocks.
