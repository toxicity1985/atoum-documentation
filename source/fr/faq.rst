.. _faq:

Questions Fréquentes
####################

.. _faq_error_log:

Si vous avec une erreur inconnue, vérifier si vous utiliser un error_log ?
**************************************************************************
Si vous utilisez `error_log`, vous rencontrerez une erreur "Error UNKNOWN in" de atoum. Pour éviter cela, utiliser :ref:`un mock d'une fonction native<mock-native-function>` de `error_log`

.. code-block:: php

	<?php
	namespace Foo
	{
		class TestErrorLog
		{
		    public function runErrorLog()
		    {
		        error_log('message');
		        return true;
		    }
		}
	}

	namespace Foo\test\unit
	{
		class TestErrorLog extends \atoum
		{
		    public function testRunErrorLog()
		    {
				$this->function->error_log = true;
				$this->newTestedInstance;
				$this->boolean($this->testedInstance->runErrorLog())->isTrue;
				$this->function('error_log')->wasCalled()->once();
		    }
		}
	}


.. _faq_ogo:

atoum s'est-il toujours appelé atoum ?
**************************************
Non, au début, atoum était nommé ogo. Lorsque vous écrivez PHP sur un clavier azerty, puis que vous décalé d'une touche vers la gauche, vous écrivez ogo.

.. _faq_license:

Quelle est la licence de atoum ?
********************************
atoum est distribué sous la licence BSD-3-Clause. Regarder le fichier de `LICENSE <https://github.com/atoum/atoum/blob/master/LICENSE>`_ embarqué pour plus de détails.

Que est la feuille de route ?
*****************************
Le plus simple est de regarder les `tags de milestone <https://github.com/atoum/atoum/milestones>`_ sur github.
