.. _mocking_systems:

Système de mocks
################

Les mocks(bouchons) sont des classes virtuels créer à la volée. Ils sont utilisé pour isolé les tests du comportements des autres classes. atoum a
un système de mock simple et puissant, permettant de générer des mocks depuis une classe ou une interface qui existe ou est virtuel,
ou encore est abstraite.

Grâce à ces bouchons, vous pourrez simuler des comportements en redéfinissant les méthodes `publiques` de vos classes. Pour les méthodes private et protected,
vous pouvez utiliser `l'extension de visibilité <http://extensions.atoum.org/extensions/visibility>`_.

.. warning::
   La plupart de méthode qui configurent le mock, s’appliquent uniquement pour la prochaine génération de ceux-ci!

.. include:: mocking_systems/mocks_generation.inc.rst
.. include:: mocking_systems/mock_behaviour.inc.rst
.. include:: mocking_systems/test_mock.inc.rst
.. include:: mocking_systems/native_functions.inc.rst
.. include:: mocking_systems/constant.inc.rst
