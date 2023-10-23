# Область видимости
Область видимости (модификаторы доступа, уровни доступа).  
Уровни доступа - для других классов.

- public - доступен везде,
- private - доступен внутри класса (например его методе), а в классах наследниках и объектах не доступен (доступен через переопределение в методе),
- protected - нет доступа

Пример:

    class Car {
      public $brand; // public доступен отовсюду
      public $color;
      private $basePrice = 100; // Доступен только в Car
      protected $hidden = 'Комментарий';

      public function __construct($brand, $color) {
        $this->brand = $brand;
        $this->color = $color;
      }

      public function getPrice() {
        return $this->basePrice * 1.2; // Коэффициент может зависеть от модели и цвета
      }

      public function getHidden() {
        return $this->hidden; // Коэффициент может зависеть от модели и цвета
      }
    }

    $car = new Car( 'Мерседес', 'Черный' );
    // echo $car->brand;     // Мерседес
    // echo $car->basePrice; // Нет доступа
    // echo $car->hidden;    // Нет доступа

    // echo $car->getPrice();  // 120
    // echo $car->getHidden(); // Комментарий

    class Mercedes extends Car {
      public $model;

      public function __construct($brand, $color, $model) {
        parent::__construct($brand, $color);
        $this->model = $model;
      }

      public function checkScope() {
        $this->brand = 'БМВ';            // есть доступ
        $this->basePrice = 150;          // есть доступ
        $this->hidden = "Комментарий 2"; // Нет доступа 
      }
    }

    $mercedesA = new Mercedes( 'Мерседес', 'Черный', 'А' );
    // echo $mercedesA->model;
    // echo $mercedesA->basePrice;   // Нет доступа
    // echo $mercedesA->getPrice();  // 120
    // echo $mercedesA->hidden;      // Нет доступа
    // echo $mercedesA->getHidden(); // Комментарий

    $mercedesA->checkScope();
    echo $mercedesA->brand;
    echo $mercedesA->basePrice;
    echo $mercedesA->hedden;
