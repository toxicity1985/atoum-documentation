.. _configuration_bootstraping:

Configuration & bootstraping
############################

When atoum start several steps will be involved, some of them can be influenced by some special files.

We can have a simplified view of theses special files with:

#. Load the autoloader file
#. Load the configuration file
#. Load the bootstrap file

.. note::
	All of theses files are optional! You can use atoum ``--init`` to generate theses files.

.. include:: configuration_bootstraping/autoloader.inc.rst
.. include:: configuration_bootstraping/configuration.inc.rst
.. include:: configuration_bootstraping/bootstrap.inc.rst
.. include:: configuration_bootstraping/having_fun_with_atoum.inc.rst
