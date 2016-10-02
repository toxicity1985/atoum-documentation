.. _configuration_bootstraping:

Configuration & bootstraping
############################

Plusieurs étapes vont se succéder au lancement d'atoum, certaines d'entre elles peuvent être influencées par des fichiers spéciaux.

On peut avoir une vue simplifiée de ces fichiers spéciaux en :

#. Chargeant l':ref:`autoloader<autoloader_file>`
#. Chargeant le :ref:`fichier de configuration<fichier-de-configuration>`
#. Chargeant le :ref:`fichier de bootstrap<bootstrap_file>`

.. note::
	Tous ces fichiers sont optionnels!

.. note::
	Vous pouvez utiliser atoum ``--init`` pour générer ces fichiers.

.. include:: configuration_bootstraping/autoloader.inc.rst
.. include:: configuration_bootstraping/configuration.inc.rst
.. include:: configuration_bootstraping/bootstrap.inc.rst
.. include:: configuration_bootstraping/amusons_nous_avec_atoum.inc.rst
