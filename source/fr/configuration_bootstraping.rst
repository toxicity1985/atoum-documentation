.. _configuration_bootstraping:

Configuration & bootstraping
############################

Plusieurs étapes vont se succéder au lancement d'atoum, Quand atoum se lance, certaines d'entre elles peuvent être influencées par des fichiers spéciaux.

On peut avoir une vue simplifiée de ces fichiers spéciaux en :

#. Chargeant le :ref:`autoloader file<autoloader_file>`
#. Chargeant le :ref:`configuration file<fichier-de-configuration>`
#. Chargeant le :ref:`bootstrap file<bootstrap_file>`

.. note::
	Tous ces fichiers sont optionnels!

.. note::
	Vous pouvez utiliser atoum ``--init`` pour générer ces fichiers.

.. include:: configuration_bootstraping/autoloader.inc.rst
.. include:: configuration_bootstraping/configuration.inc.rst
.. include:: configuration_bootstraping/bootstrap.inc.rst
.. include:: configuration_bootstraping/amusons_nous_avec_atoum.inc.rst
