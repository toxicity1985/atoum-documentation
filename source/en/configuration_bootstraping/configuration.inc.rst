.. _fichier-de-configuration:

Configuration file
******************

The configuration file is the way you can configure how atoum works.

The default name of the file is ``.atoum.php``, atoum will load it automatically if this file is located in the current directory. You can define it through the cli with ``-c``.

If you have in one of the parent directory a ``.atoum.php`` it will also be loaded. So you can have a default configuration to have the loop or debug mode activated by default.


.. _coverage-code-config:

Code coverage
=============

By default, if PHP has the extension `Xdebug <http://xdebug.org>`_, atoum indicates in command line report, the rate of tests code coverage. Some change in the behaviour of
coverage can be adapt through the :ref:`cli options<cli-options-coverage_reports>`.

If the coverage rate is 100%, atoum merely indicated. But otherwise, it displays the overall coverage and that of each method of the class tested in the form of a percentage.

.. code-block:: shell

   $ php tests/units/classes/template.php
   > atoum version DEVELOPMENT by Frederic Hardy (/Users/fch/Atoum)
   > PHP path: /usr/local/bin/php
   > PHP version:
   => PHP 5.3.8 (cli) (built: Sep 21 2011 23:14:37)
   => Copyright (c) 1997-2011 The PHP Group
   => Zend Engine v2.3.0, Copyright (c) 1998-2011 Zend Technologies
   =>     with Xdebug v2.1.1, Copyright (c) 2002-2011, by Derick Rethans
   > mageekguy\atoum\tests\units\template...
   [SSSSSSSSSSSSSSSSSSSSSSSSSSS_________________________________][27/27]
   => Test duration: 15.63 seconds.
   => Memory usage: 8.25 Mb.
   > Total test duration: 15.63 seconds.
   > Total test memory usage: 8.25 Mb.
   > Code coverage value: 92.52%
   => Class mageekguy\atoum\template: 91.14%
   ==> mageekguy\atoum\template::setWith(): 80.00%
   ==> mageekguy\atoum\template::resetChildrenData(): 25.00%
   ==> mageekguy\atoum\template::addToParent(): 0.00%
   ==> mageekguy\atoum\template::unsetAttribute(): 0.00%
   => Class mageekguy\atoum\template\data: 96.43%
   ==> mageekguy\atoum\template\data::__toString(): 0.00%
   > Running duration: 2.36 seconds.
   Success (1 test, 27 methods, 485 assertions, 0 error, 0 exception) !

However, it is possible to get a more accurate representation of the rate of code coverage by tests, in HTML report.

To get it, simply rely on models of configuration files included in atoum.

Phar users
----------

If you use the PHAR archive, it must retrieve them by using the following command:

.. code-block:: shell

   php atoum.phar -er /path/to/destination/directory

Once the extraction is done, you should have in the "directory/path/to/destination/directory" a directory called "resources/configurations/runner".

Composer users
--------------

If you are using atoum with a github repository clone :ref:`installation-par-github` or with composer :ref:`installation-par-composer`, the models can be found in ``/path/to/atoum/resources/configurations/runner``

Custom coverage reports
-----------------------

In this directory, there is, among other interesting things, a template of configuration file for atoum named ``coverage.php.dist`` that you need to copy to the location of your choice. Rename the ``coverage.php``.

After copying the file, just have to change it with the editor of your choice to define the directory where the HTML files will be generated and the URL from which the report should be accessible.

For example:

.. code-block:: php

   $coverageField = new atoum\report\fields\runner\coverage\html(
       'Code coverage of my project',
       '/path/to/destination/directory'
   );

   $coverageField->setRootUrl('http://url/of/web/site');

.. note::
   It is also possible to change the title of the report using the first argument to the constructor of the class ``mageekguy\atoum\report\fields\runner\coverage\html``.


Once this is done, you just have to use the configuration file (or include it in your configuration file) when running the tests, as follows:

.. code-block:: shell

   $ ./bin/atoum -c path/to/coverage.php -d tests/units

Once the tests run, atoum generate the code coverage report in HTML format in the directory that you set earlier, and it will be readable using the browser of your choice.

.. note::
   The calculation of code coverage by tests as well as the generation of the corresponding report may slow significantly the performance of the tests. Then it can be interesting, not to systematically use the corresponding configuration file, or disable them temporarily using the -ncc argument.

.. _reports-using:

Using standard reports
======================

atoum come with a lot of standard reports: tap, xunit, html, cli, phing, vim, ...  There is also some :ref:`fun reports<fun-with-atoum>` too. You will find the most important of them here.

.. note::
   If you want to go further, there is an :ref:`extension<extensions>` dedicated to the reports called ``reports-extension``.

.. _reports-configuration:

Report configuration
--------------------

.. _reports-configuration_path-branch:

Branch and path coverage
''''''''''''''''''''''''

You can enable the coverage of branch and path inside the configuration with ``enableBranchAndPathCoverage``. This will improve the value of the code coverage by not only
checking  the method in the code called, but also that each branch is called. To make it simple, if you have an ``if`` the coverage report will change if you check the
else. You can also enabled it with :ref:`cli option --epbc<cli-options-ebpc>`.

.. code-block:: php

   $script->enableBranchAndPathCoverage();

.. code-block:: shell

   => Class Foo\Bar: Line: 31.46%
   # with branch and path coverage
   => Class Foo\Bar: Line: 31.46% Path: 1.50% Branch: 26.06%

Disabling coverage for a class
''''''''''''''''''''''''''''''

If you want to exclude some class from coverage, you can use ``$script->noCodeCoverageForClasses(\myClass::class)``.

.. _report-html-basic:

HTML report
-----------

By default atoum provide a basic html report. For advanced html report, you should use the reports-extension.

.. code-block:: php

   <?php
   $report = $script->addDefaultReport();
   $coverageField = new atoum\report\fields\runner\coverage\html('Your Project Name', __DIR__ . '/reports');
   // Please replace in next line http://url/of/web/site by the root url of your code coverage web site.
   $coverageField->setRootUrl('http://url/of/web/site');
   $report->addField($coverageField);

.. _reports-cli:

CLI report
----------

The CLI report is the report you have when you launch the test. there is several options available

* hideClassesCoverageDetails: Will disable the coverage of the class.
* hideMethodsCoverageDetails: Will disable the coverage of the methods.

.. code-block:: php

   <?php
   $script->addDefaultReport() // in default reports there is the cli report
       ->hideClassesCoverageDetails()
       ->hideMethodsCoverageDetails();

Displaying the logo of atoum
''''''''''''''''''''''''''''

.. code-block:: php

   <?php
   $report = $script->addDefaultReport();

   // This will add the atoum logo before each run.
   $report->addField(new atoum\report\fields\runner\atoum\logo());

   // This will add a green or red logo after each run depending on its status.
   $report->addField(new atoum\report\fields\runner\result\logo());

.. _report-treemap:

Treemap report
--------------


.. code-block:: php

   <?php
   $report = $script->addDefaultReport();

   $coverageHtmlField = new atoum\report\fields\runner\coverage\html('Your Project Name', __DIR__ . '/reports');
   // Please replace in next line http://url/of/web/site by the root url of your code coverage web site.
   $coverageHtmlField->setRootUrl('http://url/of/web/site');
   $report->addField($coverageField);

   $coverageTreemapField = new atoum\report\fields\runner\coverage\treemap('Your project name', __DIR__ . '/reports');
   $coverageTreemapField
      ->setTreemapUrl('http://url/of/treemap')
      ->setHtmlReportBaseUrl($coverageHtmlField->getRootUrl());

   $report->addField($coverageTreemapField);

.. _notifications-anchor:

Notifications
=============

atoum is able to warn you when the tests are run using several notification system: `Growl`_, `Mac OS X Notification Center`_, `Libnotify`_.


Growl
-----

This feature requires the presence of the executable ``growlnotify``. To check if it is available, use the following command:

.. code-block:: shell

   $ which growlnotify

You will have the path to the executable or the message ``growlnotify not found`` if it is not installed.

Then just add the following code to your configuration file:

.. code-block:: php

   <?php
   $images = '/path/to/atoum/resources/images/logo';

   $notifier = new \mageekguy\atoum\report\fields\runner\result\notifier\image\growl();
   $notifier
       ->setSuccessImage($images . DIRECTORY_SEPARATOR . 'success.png')
       ->setFailureImage($images . DIRECTORY_SEPARATOR . 'failure.png')
   ;

   $report = $script->AddDefaultReport();
   $report->addField($notifier, array(atoum\runner::runStop));


Mac OS X Notification Center
----------------------------

This feature uses the ``terminal-notifier`` utility. To check if it is available, use the following command:

.. code-block:: shell

   $ which terminal-notifier

You will have the path to the executable or the message ``terminal-notifier not found`` if it is not installed.

.. note::
   Visit `the project's Github page <https://github.com/alloy/terminal-notifier>`_ to get more information on ``terminal-notifier``.


Then just add the following code to your configuration file:

.. code-block:: php

   <?php
   $notifier = new \mageekguy\atoum\report\fields\runner\result\notifier\terminal();

   $report = $script->AddDefaultReport();
   $report->addField($notifier, array(atoum\runner::runStop));

On OS X, you can define a command to be executed when the user clicks on the notification.

.. code-block:: php

   <?php
   $coverage = new atoum\report\fields\runner\coverage\html(
       'Code coverage',
       $path = sys_get_temp_dir() . '/coverage_' . time()
   );
   $coverage->setRootUrl('file://' . $path);

   $notifier = new \mageekguy\atoum\report\fields\runner\result\notifier\terminal();
   $notifier->setCallbackCommand('open file://' . $path . '/index.html');

   $report = $script->AddDefaultReport();
   $report
       ->addField($coverage, array(atoum\runner::runStop))
       ->addField($notifier, array(atoum\runner::runStop))
   ;

The example above shows how to automatically open the code coverage report when the user clicks on the notification.


Libnotify
---------

This feature requires the presence of the executable ``notify-send``. To check if it is available, use the following command:

.. code-block:: shell

   $ which notify-send

You will have the path to the executable or the message ``notify-send not found`` if it is not installed.

Then just add the following code to your configuration file:

.. code-block:: php

   <?php
   $images = '/path/to/atoum/resources/images/logo';

   $notifier = new \mageekguy\atoum\report\fields\runner\result\notifier\image\libnotify();
   $notifier
       ->setSuccessImage($images . DIRECTORY_SEPARATOR . 'success.png')
       ->setFailureImage($images . DIRECTORY_SEPARATOR . 'failure.png')
   ;

   $report = $script->AddDefaultReport();
   $report->addField($notifier, array(atoum\runner::runStop));

.. _configuration-test:

Configuration of the test
=========================
A lot of possibility to configure how atoum will find and execute the test is available. You can use the arguments in the cli or the configuration file.
Because, a simple code will explain a lot more than a long text, just read this:

.. code-block:: php

   <?php
   $testGenerator = new atoum\test\generator();

   // your unit test's directory. (-d)
   $testGenerator->setTestClassesDirectory(__DIR__ . '/test/units');

   // your unit test's namespace.
   $testGenerator->setTestClassNamespace('your\project\namespace\tests\units');

   // your unit test's runner.
   $testGenerator->setRunnerPath('path/to/your/tests/units/runner.php');

   $script->getRunner()->setTestGenerator($testGenerator);
   // or
   $runner->setTestGenerator($testGenerator);

You can also define the directory of your test with ``$runner->addTestsFromDirectory(path)``. atoum will load all the class that can be tested from this directory like you can do
with :ref:`-d<cli-options-directories>` argument in cli.

.. code-block:: php

   <?php
   $runner->addTestsFromDirectory(__DIR__ . '/test/units');
