.. _ide_integration:

Integration of atoum in your IDE
################################

.. _ide_sublime2:

Sublime Text 2
**************

A `plug-in for SublimeText 2 <https://github.com/toin0u/Sublime-atoum>`_ allows the execution of unit tests by atoum and the visualization of the results without leaving the editor.

The information necessary for its installation and its configuration are available `on the blog's author <http://sbin.dk/2012/05/19/atoum-sublime-text-2-plugin/>`_.

.. _ide_vim:

VIM
***

atoum comes with a plug-in for VIM.

It lets you run tests and obtain a report in a separate window without leaving VIM.

It's possible to navigate through errors, or even to go to the line in the editor with an assertion from failed test with a simple combination of keystrokes.


Installation of the plug-in atoum for VIM
=========================================

You will find the file corresponding to the plug-in, named ``atoum.vmb`` inside the `dedicated repository <https://github.com/atoum/vim-plugin>`_.
Once you have the ``atoum.vmb`` file, you need to edit it with VIM:

.. code-block:: shell

   $ vim path/to/atoum.vmb

Now install the plug-in by using the command in VIM:

.. code-block:: vim

   :source %


Use of the atoum plug-in for VIM
================================

To use the plug-in, atoum must be installed and you must be editing a file containing a class of unit tests based on atoum.

Once configured, the following command will launch the execution of tests:

.. code-block:: vim

   :Atoum

The tests will be executed, and once finished, a report based on the configuration of atoum file located in the directory ``ftplugin/php/atoum.vim`` in your ``.vim`` directory is generated in a new window.

Of course, you are free to bind this command to any combination of keystrokes of your choice, for example adding the following line in your ``.vimrc`` file:

.. code-block:: vim

   nnoremap *.php <F12> :Atoum<CR>

``F12`` in normal mode will call the command ``:Atoum``.


Configuration file management of atoum
========================================

You can specify another configuration file for atoum by adding the following line to your ``.vimrc`` file:

.. code-block:: vim

   call atoum#defineConfiguration('/path/to/project/directory', '/path/to/atoum/configuration/file', '.php')

Indeed the function ``atoum#defineConfiguration`` lets you configure the file to use, based on the directory where the unit test files are located.
It take three arguments:

* a path to the directory containing the unit tests;
* a path to the configuration file of atoum to be used;
* the extension's file of relevant unit tests.

You can access help about the plug-in in VIM with the following command:

.. code-block:: vim

   :help atoum

Coverage reports inside vim
===========================

You can configure a specific :ref:`report<reports-using>` for the coverage in vim. In your atoum configuration file, set:

.. code-block:: php

   <?php
   use \atoum\atoum;
   $vimReport = new atoum\reports\asynchronous\vim();
   $vimReport->addWriter($stdOutWriter);
   $runner->addReport($vimReport);

.. _ide_phpstorm:

PhpStorm
********

atoum comes with an official plug-in for PHPStorm. It really helps you in your day-to-day development. The main functionality are:

* Go to the test class from the tested class (shortcut : alt+shift+K)
* Go to the tested class from the test class (shortcut : alt+shift+K)
* Execute tests inside PhpStorm (shortcut : alt+shift+M)
* Easily identify test files by a custom icon

Installation
============

It's easy to install, simply follow theses steps:

* Open PhpStorm
* Go to *File -> Settings*, then click on *Plugins*
* Click on Browse repositories
* Search for *atoum* in the list, then click on the install button
* Restart PhpStorm

If you need more information check the `repository of the plugins <https://github.com/atoum/phpstorm-plugin>`_.

.. _ide_atom:

Atom
****

atoum comes with an official package for atom. It helps you in several tasks:

* A panel with all tests
* Run all the tests, a directory or the current one

Installation
============

It's easy to install, simply follow the `official documentation <http://flight-manual.atom.io/using-atom/sections/atom-packages/>`_ or theses steps:

* Open atom
* Go to *Settings*, then click on *Install*
* Search for *atoum* in the list, then click on the install button

If you need more information check the `repository of the package <https://github.com/atoum/atom-plugin>`_.


.. _ide_netbeans:

netbeans
********

atoum is officially integrated into netbeans since a long time, so you have nothing to do. Check this tutorial on `how to use netbeans with atoum <https://github.com/atoum/netbeans-sample>`_.

.. _ide_auto-open-test:

Automatically open failed tests
*******************************

atoum is able to automatically open files from failed tests at the end of there execution. Several editors are currently supported:

* :ref:`macvim<ide_auto-open_macvim>` (Mac OS X)
* :ref:`gvim<ide_auto-open_gvim>` (Unix)
* :ref:`PhpStorm<ide_auto-open_phpstorm>` (Mac OS X/Unix)
* :ref:`gedit<ide_auto-open_gedit>` (Unix)

To use this feature, you need to change the :ref:`configuration file <fichier-de-configuration>` following you ide:

.. note::
	You also simplfy you life using an `extension that do it for you <http://extensions.atoum.org/extensions/atoum-ide-helper>`_.

.. _ide_auto-open_macvim:

macvim
======

.. code-block:: php

   <?php
   use
       atoum\atoum,
       atoum\atoum\report\fields\runner\failures\execute\macos
   ;

   $stdOutWriter = new atoum\writers\std\out();
   $cliReport = new atoum\reports\realtime\cli();
   $cliReport->addWriter($stdOutWriter);

   $cliReport->addField(new macos\macvim());

   $runner->addReport($cliReport);

.. _ide_auto-open_gvim:

gvim
====

.. code-block:: php

   <?php
   use
       atoum\atoum,
       atoum\atoum\report\fields\runner\failures\execute\unix
   ;

   $stdOutWriter = new atoum\writers\std\out();
   $cliReport = new atoum\reports\realtime\cli();
   $cliReport->addWriter($stdOutWriter);

   $cliReport->addField(new unix\gvim());

   $runner->addReport($cliReport);

.. _ide_auto-open_phpstorm:

PhpStorm
========

If you are under Mac OS X, use the following configuration:

.. code-block:: php

   <?php
   use
       atoum\atoum,
       atoum\atoum\report\fields\runner\failures\execute\macos
   ;

   $stdOutWriter = new atoum\writers\std\out();
   $cliReport = new atoum\reports\realtime\cli();
   $cliReport->addWriter($stdOutWriter);

   $cliReport
       // If PhpStorm is installed in /Applications
       ->addField(new macos\phpstorm())

       // If you have installed PhpStorm
       // in another directory than /Applications
       // ->addField(
       //     new macos\phpstorm(
       //         '/path/to/PhpStorm.app/Contents/MacOS/webide'
       //     )
       // )
   ;

   $runner->addReport($cliReport);


Under Unix environment, use the following configuration:

.. code-block:: php

   <?php
   use
       atoum\atoum,
       atoum\atoum\report\fields\runner\failures\execute\unix
   ;

   $stdOutWriter = new atoum\writers\std\out();
   $cliReport = new atoum\reports\realtime\cli();
   $cliReport->addWriter($stdOutWriter);

   $cliReport
       ->addField(
           new unix\phpstorm('/path/to/PhpStorm/bin/phpstorm.sh')
       )
   ;

   $runner->addReport($cliReport);

.. _ide_auto-open_gedit:

gedit
=====

.. code-block:: php

   <?php
   use
       atoum\atoum,
       atoum\atoum\report\fields\runner\failures\execute\unix
   ;

   $stdOutWriter = new atoum\writers\std\out();
   $cliReport = new atoum\reports\realtime\cli();
   $cliReport->addWriter($stdOutWriter);

   $cliReport->addField(new unix\gedit());

   $runner->addReport($cliReport);
