.. _annotation-php-extension:

PHP Extensions
**************

Certains des tests peuvent requérir une ou plusieurs extensions PHP. atoum permet de définir cela directement à travers une annotation ``@extensions``. Après l'annotation ``@extensions``, ajouter simplement le nom d'une ou plusieurs extensions, séparés par une virgule.


.. code-block:: php

   <?php

   namespace vendor\project\tests\units;

   class foo extends \atoum
   {
       /**
        * @extensions intl
        */
       public function testBar()
       {
           // ...
       }
   }

Le test ne sera exécuté que si l'extension intl est présente. Dans le cas contraire, le test sera passé et le message suivant sera affiché.

.. code-block:: shell

   vendor\project\tests\units\foo::testBar(): PHP extension 'intl' is not loaded


.. note::
   Par défaut, le test est validé lorsqu'il a été passé. Mais vous pouvez utiliser :ref:`--fail-if-skipped-methods<cli-opts-fail-if-skipped-methods>` l'option de la ligne de commande afin de faire échouer les tests passés.

