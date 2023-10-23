# Объект
Чтобы получить доступ к данным класса, нужно создать объект этого класса.

## Создание объекта

    class Person {
      public $name = 'Ivan';
      public $age = 21;
      public $isMarried = true;

      public function getName() {
        return $this->name;
      }
    }

    $ivan = new Person();
    echo $ivan->name;      // доступ к свойству
    echo $ivan->getName(); // доступ к методу

В переменной `$ivan` хранятся все свойства и методы класса.  
При обащении к свойству, знак доллара опускаем: `$ivan->name`.
