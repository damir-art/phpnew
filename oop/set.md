# Сеттер
Сеттер - это метод получающий параметр и изменяющий данные объекта.

    class Person {
      public $name;

      public function setName($name) {
        return $this->name = $name;
      }
    }

    $ivan = new Person();
    echo $ivan->setName('Иван'); // Иван

    $petr = new Person();
    echo $ivan->setName('Петр'); // Петр
