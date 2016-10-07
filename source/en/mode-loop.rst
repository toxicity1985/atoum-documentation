
.. _mode-loop:

Loop mode
#########

When a developer is doing TDD (Test-Driven Development), it usually works as follows:

#. Start writing a test corresponding to what they want to develop,
#. run the test created,
#. write the code to pass the test,
#. then amend or complete the test and go back to step 2.

In practice, this means that they must:

* Create the code in their favourite editor,
* exit the editor and run the test in a console,
* return to their editor to write the code that enables the test to pass,
* return to the console to restart the test execution,
* return to their editor in order to amend or supplement its test

There is therefore a cycle that will be repeated until the functionality is complete.

During this cycle, the developer must repeatedly run the same terminal command to run the unit tests.

atoum offers the ``loop`` mode via the arguments ``-l`` or ``--loop``, which lets the developer avoid restarting the test manually and streamline the development process.

In this mode, atoum runs the required tests.

Once the tests are complete, if the tests passed, atoum simply waits:

.. code-block:: shell

   $ php tests/units/classes/adapter.php -l
   > PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [SS__________________________________________________________][2/2]
   => Test duration: 0.00 second.
   => Memory usage: 0.50 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.50 Mb.
   > Running duration: 0.05 second.
   Success (1 test, 2/2 methods, 0 void method, 0 skipped method, 4 assertions)!
   Press <Enter> to reexecute, press any other key and <Enter> to stop...


If the developer presses the ``Enter`` key, atoum will reexecute the same test, without any other action from the developer.

In the case where the code doesn't pass the tests successfully, i.e. if assertions fails or if there were errors or exceptions, atoum also starts waiting :

.. code-block:: shell

   $ php tests/units/classes/adapter.php -l> PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [FS__________________________________________________________][2/2]
   => Test duration: 0.00 second.
   => Memory usage: 0.25 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.25 Mb.
   > Running duration: 0.05 second.
   Failure (1 test, 2/2 methods, 0 void method, 0 skipped method, 0 uncompleted method, 1 failure, 0 error, 0 exception)!
   > There is 1 failure:
   => mageekguy\atoum\tests\units\adapter::test__call():
   In file /media/data/dev/atoum-documentation/tests/vendor/atoum/atoum/tests/units/classes/adapter.php on line 16, mageekguy\atoum\asserters\string() failed: strings are not equal
   -Expected
   +Actual
   @@ -1 +1 @@
   -string(32) "1305beaa8f3f2f932f508d4af7f89094"
   +string(32) "d905c0b86bf89f9a57d4da6101f93648"
   Press <Enter> to reexecute, press any other key and <Enter> to stop...


If the developer presses the ``Enter`` key, instead of replaying the same tests again, atoum will only execute the tests that have failed, rather than replaying them all.

The developer can pops issues and replay error tests as many times as necessary simply by pressing ``Enter``.

Once all failed tests pass successfully, atoum will automatically run all test suites to detect any potential regressions introduced by the corrections made by the developer.

.. code-block:: shell

   Press <Enter> to reexecute, press any other key and <Enter> to stop...
   > PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [S___________________________________________________________][1/1]
   => Test duration: 0.00 second.
   => Memory usage: 0.25 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.25 Mb.
   > Running duration: 0.05 second.
   Success (1 test, 1/1 method, 0 void method, 0 skipped method, 2 assertions)!
   > PHP path: /usr/bin/php
   > PHP version:
   => PHP 5.6.3 (cli) (built: Nov 13 2014 18:31:57)
   => Copyright (c) 1997-2014 The PHP Group
   => Zend Engine v2.6.0, Copyright (c) 1998-2014 Zend Technologies
   > mageekguy\atoum\tests\units\adapter...
   [SS__________________________________________________________][2/2]
   => Test duration: 0.00 second.
   => Memory usage: 0.50 Mb.
   > Total test duration: 0.00 second.
   > Total test memory usage: 0.50 Mb.
   > Running duration: 0.05 second.
   Success (1 test, 2/2 methods, 0 void method, 0 skipped method, 4 assertions)!
   Press <Enter> to reexecute, press any other key and <Enter> to stop...


Of course, the ``loop`` mode will take only :ref:`the files with unit tests launch <fichiers-a-executer>` by atoum.
