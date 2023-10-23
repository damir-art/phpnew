# Интерфейс
Интерфейс - список методов которые обязательно нужно реализовать. В интерфейсе описывается только сигнатура метода, а не тело. Интерфейсы нужны для того чтобы архитектор один раз создал интерфейс  с нужными методами, а мидлы потом создавали от него классы.

    interface Sport {
      public function walk();
      public function run();
      public function sleep();
    }

    class Boxing implements Sport {
      public function walk() {
        return 'Ходить';
      }
      public function run() {
        return 'Бежать';
      }
      public function sleep() {
        return 'Спать';
      }
    }

    $box = new Boxing();
    echo $box->walk();
