.. _configuration_bootstraping:

Configuration & bootstraping
############################

When atoum start, several steps will be involved, some of them can be influenced by some special files.

We can have a simplified view of theses special files with:

#. Load the :ref:`autoloader file<autoloader_file>`
#. Load the :ref:`configuration file<fichier-de-configuration>`
#. Load the :ref:`bootstrap file<bootstrap_file>`

.. note::
	All of theses files are optional!

.. note::
	You can use atoum ``--init`` to generate theses files.

.. include:: configuration_bootstraping/autoloader.inc.rst
.. include:: configuration_bootstraping/configuration.inc.rst
.. include:: configuration_bootstraping/bootstrap.inc.rst
.. include:: configuration_bootstraping/having_fun_with_atoum.inc.rst
