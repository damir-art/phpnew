# Наследование
Наследование классов.  
Наследование наследуются свойства и методы, сокращает код.

## Без конструктора

    class Person {
      public $name = 'Иван';
      public $age = 21;

      function getAge() {
        return $this->age;
      }
    }

    class PersonDev extends Person {
      public function job() {
        return 'Программист';
      }
    }

    $ivan = new PersonDev();
    echo $ivan->name; // Иван
    echo $ivan->getAge(); // 21
    echo $ivan->job(); // Программист

## С конструктором
Конструктор тоже наследуется:

    class Person {
      public $name;
      public $age;

      public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
        echo 'Конструктор класса родителя.' . '<br />';
      }
    }

    class PersonJob extends Person {
      public $job = 'Dev';
      public function getJob() {
        return $this->job;
      }
    }

    $ivan = new PersonJob('Иван', 21);
    echo $ivan->name; // Иван
    echo $ivan->age; // 21
    echo $ivan->job; // Dev
    echo $ivan->getJob(); // Dev

## Конструктор в наследнике
Конструктор в классе наследнике:

    class Person {
      public $name;
      public $age;

      public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
        echo 'Конструктор класса родителя.' . '<br />';
      }
    }

    class PersonDev extends Person {
      public $dev;

      public function __construct($name, $age, $dev) {
        // Обращение к родительскому конструктору
        parent::__construct($name, $age);
        $this->dev = $dev;
        echo 'Конструктор класса наследника.' . '<br />';
      }

      public function getDev() {
        return $this->dev;
      }
    }

    $ivan = new PersonDev('Иван', 21, 'PHP');
    echo $ivan->name . '<br >'; // Иван
    echo $ivan->age . '<br />'; // 21
    echo $ivan->dev . '<br />'; // PHP
    echo $ivan->getDev(); // PHP

## Перезапись конструктора
Перезапись родительского конструктора в наследнике:

    class PersonDev extends Person {
      public $dev;

      // Перезапись родительского конструктора
      public function __construct($dev) {
        $this->dev = $dev;
        echo 'Перезапись родительского конструктора.' . '<br />';
      }

      public function getDev() {
        return $this->dev;
      }
    }

    $ivan = new PersonDev('PHP');
    echo $ivan->dev . '<br />'; // PHP
    echo $ivan->getDev(); // PHP
