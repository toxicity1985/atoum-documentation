.. _contribute:

Participer
==========

.. _how-to-contribute:

Comment participer
------------------------

.. important::
   We need help to write this section !


.. _convention-de-codage:

Convention de codage
------------------------
Le code source d'atoum respecte certaines conventions. Si vous souhaitez contribuer au projet, votre code devra respecter ces mêmes règles :

* L'indentation est faite avec le caractère de tabulation,
* Les noms des espaces de noms, classes, membres, méthodes et constantes sont en ``lowerCamelCase``,
* Le code doit être testé.

L'exemple ci-dessous n'a aucun sens, mais il permet de présenter plus en détail la manière dont le code est écrit :

.. code-block:: php

   <?php

   namespace atoum\atoum\coding;

   use
       atoum\atoum,
       type\hinting
   ;

   class standards
   {
       const standardsConst = 'standardsConst';
       const secondStandardsConst = 'secondStandardsConst';

       public $public;
       protected $protected;
       private $private = array();

       public function publicFunction($parameter, hinting\claass $optional = null)
       {
           $this->public = trim((string) $parameter);
           $this->protected = $optional ?: new hinting\claass();

           if (($variable = $this->protectedFunction()) === null)
           {
               throw new atoum\exception();
           }

           $flag = 0;
           switch ($variable)
           {
               case self::standardsConst:
                   $flag = 1;
                   break;

               case self::standardsConst:
                   $flag = 2;
                   break;

               default:
                   return null;
           }

           if ($flag < 2)
           {
               return false;
           }
           else
           {
               return true;
           }
       }

       protected function protectedFunction()
       {
           try
           {
               return $this->protected->get();
           }
           catch (atoum\exception $exception)
           {
               throw new atoum\exception\runtime();
           }
       }

       private function privateFunction()
       {
           $array = $this->private;

           return function(array $param) use ($array) {
               return array_merge($param, $array);
           };
       }
   }


Voici également un exemple de test unitaire :

.. code-block:: php

   <?php

   namespace tests\units\atoum\atoum\coding;

   use
       atoum\atoum,
       atoum\atoum\coding\standards as testedClass
   ;

   class standards extends atoum\test
   {
       public function testPublicFunction()
       {
           $this
               ->if($object = new testedClass())
               ->then
                   ->boolean($object->publicFunction(testedClass::standardsConst))->isFalse()
                   ->boolean($object->publicFunction(testedClass::secondStandardsConst))->isTrue()
               ->if($mock = new \mock\type\hinting\claass())
               ->and($this->calling($mock)->get = null)
               ->and($object = new testedClass())
               ->then
                   ->exception(function() use ($object) {
                               $object->publicFunction(uniqid());
                           }
                       )
                           ->IsInstanceOf('\\atoum\\atoum\\exception')
           ;
       }
   }

