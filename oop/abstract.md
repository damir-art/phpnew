# Абстрактный класс
Абстрактный класс запрещает создавать объекты от этого класса, но разрешает создавать классы наследники. У классов наследников абстрактного класса можно создавать объекты.

    abstract class Person {
      public $name;
      public $age;

      public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
      }
    }

Пример:

    abstract class Person {
      public $name;
      public $age;

      public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
        echo 'Конструктор абстрактного класса.' . '<br />';
      }

      public function getName() {
        return $this->name;
      }
    }

    class PersonDev extends Person {
      public $dev;

      public function __construct($name, $age, $dev) {
        parent::__construct($name, $age);
        $this->dev = $dev;
        echo 'Конструктор класса наследника.' . '<br />';
      }
    }

    $personDev = new PersonDev('Иван', 21, 'PHP');
    echo $personDev->name . '<br />';
    echo $personDev->age . '<br />';
    echo $personDev->dev . '<br />';
    echo $personDev->getName();
