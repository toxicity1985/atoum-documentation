.. _configuration_bootstraping:

Configuration & bootstraping
############################

Plusieurs étapes vont se succéder au lancement d'atoum, certaines d'entre elles peuvent être influencées par des fichiers spéciaux.

On peut avoir une vue simplifiée de ces fichiers spéciaux et *optionnelle* en :

#. Chargement de l':ref:`autoloader<autoloader_file>`
#. Chargement du :ref:`fichier de configuration<fichier-de-configuration>`
#. Chargement du :ref:`fichier de bootstrap<bootstrap_file>`

.. note::
	Vous pouvez utiliser atoum :ref:`--init<cli-options-init>` pour générer ces fichiers.

.. include:: configuration_bootstraping/autoloader.inc.rst
.. include:: configuration_bootstraping/configuration.inc.rst
.. include:: configuration_bootstraping/bootstrap.inc.rst
.. include:: configuration_bootstraping/amusons_nous_avec_atoum.inc.rst
