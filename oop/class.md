# Класс
Класс - сохраняем в переменную данные и действия.

## Создание класса
Имена классов пишут с большой буквы.

    class Person {

    }

## Создание свойства класса

    class Person {
      public $name = 'Ivan';
    }

## Создание метода класса

    class Person {
      public $name = 'Ivan';

      public function getName() {
        return $this->name;
      }
    }
