# Геттер
Геттер - это метод возвращающий данные объекта.

    class Person {
      public $name = 'Иван';

      public function getName() {
        return $this->name;
      }
    }

    $ivan = new Person();
    echo $ivan->getName(); // Иван
