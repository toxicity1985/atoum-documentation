
.. _cookbook_utilisation_behat:

Use in behat
************

The *asserters* from atoum are very easy to use outside your traditional unit tests. Just import the class *atoum\atoum\asserter* without forgetting to load the required classes (atoum provides an autoload class available in *classes/autoloader.php*).
The following example illustrates this usage of asserter from atoumin your Behat *steps*.

Installation
============

Simply install atoum and Behat in your project via pear, git clone, zip... Here is an example with dependency manager *Composer* :

.. code-block:: json

   "require-dev": {
           "behat/behat": "2.4@stable",
           "atoum/atoum": "~2.5",
   }

It is obviously mandatory to update  your composer dependencies with the command :

.. code-block:: shell

   $ php composer.phar update


Configuration
=============

As mentioned in the introduction, just import the asserter classes from atoum and ensure that they are loaded. For Behat, configuration of asserters are done inside the class *FeatureContext.php* (located by default in your directory */root-of-project/features/bootstrap/*).

.. code-block:: php

   <?php

   use Behat\Behat\Context\ClosuredContextInterface,
       Behat\Behat\Context\TranslatedContextInterface,
       Behat\Behat\Context\BehatContext,
       Behat\Behat\Exception\PendingException,
       Behat\Behat\Context\Step;
   use Behat\Gherkin\Node\PyStringNode,
       Behat\Gherkin\Node\TableNode;

   use atoum\asserter; // <- atoum asserter

   require_once __DIR__ . '/../../vendor/atoum/atoum/classes/autoloader.php'; // <- autoload

   class FeatureContext extends BehatContext
   {
       private $assert;

       public function __construct(array $parameters)
       {
           $this->assert = new asserter\generator();
       }
   }


Usage
=====

After these 2 particular trivial steps, your *steps* can be extended with the atoum asserters :

.. code-block:: php

   <?php

   // ...

   class FeatureContext extends BehatContext
   {//...

       /**
        * @Then /^I should get a good response using my favorite "([^"]*)"$/
        */
       public function goodResponse($contentType)
       {
           $this->assert
               ->integer($response->getStatusCode())
                   ->isIdenticalTo(200)
               ->string($response->getHeader('Content-Type'))
                   ->isIdenticalTo($contentType);
       }
   }

Once again, this is only an example specific to Behat but it remains valid for all needs of using the asserters of atoum outside the initial context.



.. _cookbook_utilisation_ci:

Use with continous integration tools (CI)
*****************************************

.. _cookbook_utilisation_jenkins:

Use inside Jenkins (or Hudson)
==============================

It's very simple to  the results of atoum to `Jenkins <http://jenkins-ci.org/>`_ (or `Hudson <http://hudson-ci.org/>`_) as xUnit results.


Step1: Add a xUnit report to the configuration of atoum
-------------------------------------------------------

Like other coverage report, you can use specific :ref:`report<reports-using>` from the configuration.

If you don't have a configuration file
""""""""""""""""""""""""""""""""""""""

If you don't have a configuration file for atoum yet, we recommend that you extract the directory resource of atoum in that one of your choice by using the following command :

* If you are using the Phar archive of atoum :

.. code-block:: shell

   $ php atoum.phar --extractRessourcesTo /tmp/atoum-src
   $ cp /tmp/atoum-src/resources/configurations/runner/xunit.php.dist /my/project/atoum.php

* If you are using the sources of atoum :

.. code-block:: shell

   $ cp /path/to/atoum/resources/configurations/runner/xunit.php.dist /my/project/.atoum.php

* You can also directly copy the files from `the Github repository <https://github.com/atoum/atoum/blob/master/resources/configurations/runner/xunit.php.dist>`_

There is one last step, edit this file to set the path to the xUnit report where atoum will generate it. This file is ready to use, with him, you will keep the default report and gain a xUnit report for each launch of tests.


If you already have a configuration file
""""""""""""""""""""""""""""""""""""""""

If you already have a configuration file, simply add the following lines:

.. code-block:: php

   <?php

   //...

   /*
    * Xunit report
    */
   $xunit = new atoum\reports\asynchronous\xunit();
   $runner->addReport($xunit);

   /*
    * Xunit writer
    */
   $writer = new atoum\writers\file('/path/to/the/report/atoum.xunit.xml');
   $xunit->addWriter($writer);


Step 2: Test the configuration
------------------------------

To test this configuration, simply run atoum specifying the configuration file you want to use :

.. code-block:: shell

   $ ./bin/atoum -d /path/to/the/unit/tests -c /path/to/the/configuration.php

.. note::
   If you named your configuration file  ``.atoum.php``, it will be load automatically. The ``-c`` parameter is optional in this case.
   To let atoum load automatically the ``.atoum.php`` file, you will need to run test from the folder where this file resides or one of his childs.

At the end of the tests, you will have the xUnit report inside the folder specified in the configuration.


Step 3: Launching tests via Jenkins (or Hudson)
-----------------------------------------------

There are several possibilities depending on how you build your project :

* If you use a script, simply add the previous command.
* If you use a utility tool like `phing <https://www.phing.info/>`_ or `ant <http://ant.apache.org/>`_, simply add an exec task like :

.. code-block:: xml

   <target name="unitTests">
     <exec executable="/usr/bin/php" failonerror="yes" failifexecutionfails="yes">
       <arg line="/path/to/atoum.phar -p /path/to/php -d /path/to/test/folder -c /path/to/atoumConfig.php" />
     </exec>
   </target>

Notice the addition of ``-p /path/to/php`` that permit to atoum to know the path to the php binary to use to run the unit tests.


Step 4: Publish the report with Jenkins (or Hudson)
---------------------------------------------------

Simply enable the publication of report with JUnit or xUnit format of the plugin you are using, specifying the path to the file generated by atoum.



.. _cookbook_utilisation_travis-ci:

Use with Travis-CI
==================

It's simple to use atoum with a tool like `Travis-CI <https://travis-ci.org>`_. Indeed, all the steps are described in the `travis documentation <http://docs.travis-ci.com/user/languages/php/#Working-with-atoum>`_ :
* Create your .travis.yml in your project;
* Add it the next two lines:

.. code-block:: yaml

   before_script: wget http://downloads.atoum.org/nightly/atoum.phar
   script: php atoum.phar


Here is an example file `.travis.yml` where the unit tests in the `tests` folder will be run.

.. code-block:: yaml

   language: php
   php:
     - 5.4
     - 5.5
     - 5.6

   before_script: wget http://downloads.atoum.org/nightly/atoum.phar
   script: php atoum.phar -d tests/


.. _cookbook_utilisation_phing:

Use with `Phing <https://www.phing.info/>`_
*******************************************

atoum test suite can be easily ran inside your phing configuration using the integrated *phing/AtoumTask.php* task.
A valid build example can be found in the `resources/phing/build.xml <https://github.com/atoum/atoum/blob/master/resources/phing/build.xml>`_ file.

You must register the custom task using the `taskdef <https://www.phing.info/docs/guide/stable/TaskdefTask.html>`_ native phing task :

.. code-block:: xml

  <taskdef name="atoum" classpath="vendor/atoum/atoum/resources/phing" classname="AtoumTask"/>

Then you can use it inside one of your buildfile target:

.. code-block:: xml

    <target name="test">
      <atoum
        atoumautoloaderpath="vendor/atoum/atoum/classes/autoloader.php"
        phppath="/usr/bin/php"
        codecoverage="true"
        codecoveragereportpath="reports/html/"
        showcodecoverage="true"
        showmissingcodecoverage="true"
        maxchildren="5"
      >
        <fileset dir="tests/units/">
          <include name="**/*.php"/>
        </fileset>
      </atoum>
    </target>

The paths given in these examples have been taken from a standard composer installation. All the possible parameters
are defined below, you can change values or omit some to rely on defaults. There is three kind of parameters:

atoum configurations
====================

- :ref:`bootstrap<bootstrap_file>`: Bootstrap file to be included before executing each test method

  - default: ``.bootstrap.atoum.php``
- :ref:`atoumpharpath<archive-phar>`: If atoum is used as phar, path to the phar file
- :ref:`atoumautoloaderpath<autoloader_file>`: Autoloader file before executing each test method

  - default: ``.autoloader.atoum.php``
- :ref:`phppath<cli-options-php>`: Path to ``php`` executable
- :ref:`maxchildren<cli-options-max_children_number>`: Maximum number of sub-processus which will be run simultaneously

Flags
=====

- `codecoverage`: Enable code coverage (only possible if XDebug in installed)

  - default: ``false``
- `showcodecoverage`: Display code coverage report

  - default: ``true``
- `showduration`: Display test execution duration

  - default: ``true``
- `showmemory`: Display consumend memory

  - default: ``true``
- `showmissingcodecoverage`: Display missing code coverage

  - default: ``true``
- `showprogress`: Display test execution progress bar

  - default: ``true``
- `branchandpathcoverage`: Enable branch and path coverage

  - default: ``false``
- `telemetry <http://extensions.atoum.org/extensions/telemetry>`_: Enable telemetry report (`atoum/reports-extension` must be installed)

  - default: ``false``

Reports
=======

- `codecoveragexunitpath`: Path to xunit report file
- `codecoveragecloverpath`: Path to clover report file
- :ref:`Code Coverage Basic<report-html-basic>`

  - `codecoveragereportpath`: Path to HTML report
  - `codecoveragereporturl`: URL to HTML report
- :ref:`Code Coverage Tree Map<report-treemap>`:

  - `codecoveragetreemappath`: Path to tree map
  - `codecoveragetreemapurl`: URL to tree map
- `Code Coverage Advanced <http://extensions.atoum.org/extensions/reports>`_

  - `codecoveragereportextensionpath`: Path to HTML report
  - `codecodecoveragereportextensionurl`: URL to HTML report
- `Telemetry <http://extensions.atoum.org/extensions/telemetry>`_

  - `telemetryprojectname`: Name of telemetry report to be sent
