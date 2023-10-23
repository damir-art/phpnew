# Конструктор
Вместо создания сеттера для каждого свойства, можно использовать конструктор.  
При создании объекта, конструктор запускается автоматически.

    class Person {
      public function __construct($name, $age, $isMarried) {
        $this->name = $name;
        $this->age = $age;
        $this->isMarried = $isMarried;
      }
    }

    $ivan = new Person( 'Иван', 21, true );
    echo $ivan->name . '<br />'; // Иван
    echo $ivan->age . '<br />'; // 21
    echo $ivan->isMarried; // 1

Свойства уже могут быть:

    class Person {
      public $name = 'Иван';
      public $age;

      public function __construct($name, $age, $isMarried) {
        $this->name = $name;
        $this->age = $age;
        $this->isMarried = $isMarried;
      }
    }

В конструкторе можно записать любой код:

    public function __construct($name, $age, $isMarried) {
      $this->name = $name;
      $this->age = $age;
      $this->isMarried = $isMarried;
      echo 'Конструктор отработал';
    }
