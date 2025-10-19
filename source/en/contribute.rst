.. _contribute:

Contribute
==========

.. _how-to-contribute:

How to contribute
------------------

.. important::
   We need help writing this section!


.. _convention-de-codage:

Coding convention
--------------------
The source code of atoum follows some conventions. If you wish to contribute to this project, your code must follow the same rules:

* Indentation must be done with tabs,
* Namespaces, classes, members, methods, and constants follow the ``lowerCamelCase`` convention,
* Code must be tested.

The example below makes no sense but shows in more in detail the way in which the code is written:

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


Also here is an example of an unit test:

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

