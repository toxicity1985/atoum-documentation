.. _mocking_systems:

Mocking systems
###############

Mocks are virtual class, created on the fly. They are used to isolate your test from the behaviour of the other classes. atoum has
a powerful and easy-to-implement mock system allowing you to generate mocks from classes or interfaces that exist, are virtual,
are abstract or an interface.

With these mocks, you can simulate behaviours by redefining the `public` methods of your classes. For the private & protected method,
use the `visibility extension <http://extensions.atoum.org/extensions/visibility>`_.

.. warning::
   Most of method that configure the mock, apply only for the next mock generation!

.. include:: mocking_systems/mocks_generation.inc.rst
.. include:: mocking_systems/mock_behaviour.inc.rst
.. include:: mocking_systems/test_mock.inc.rst
.. include:: mocking_systems/native_functions.inc.rst
.. include:: mocking_systems/constant.inc.rst
