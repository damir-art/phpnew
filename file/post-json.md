# post json
Сохранение данных из формы в JSON-файл.  
Форма обратной связи. Можно после отправки емаил, также сохранить данные из формы где либо: файл, БД, облако и т.п. `addApp()`.

Файловая структура проекта:
- index.php
- admin.php
- model/ - хранит функции разделённые по сущностям
  - model/apps.php
- db/
  - db/apps.txt

## index.php
Точка входа, контролер. Код должен быть максимально абстрактный, не зависящий от того например куда сохраняются данные в файл или БД. Просто вызываешь функцию на сохранение, а функция уже сама это делает. Если меняется хранилище, то меняется лишь функция сохранения в БД, а не файл index.php.

    <?php
    // Подключаем файлы с функциями
    include_once( 'model/apps.php' );

    // var_dump(getApps()); // Проверяем рабту функции получения данных

    $isSend = false;
    $err = '';

    if ( $_SERVER['REQUEST_METHOD'] === 'POST' ) {
      $name = trim( $_POST['name'] );
      $phone = trim( $_POST['phone'] );

      if ( $name === '' || $phone === '' ) {
        $err = 'Заполните все поля!';
      }
      else if ( mb_strlen($name, 'UTF8') < 2 ) {
        $err = 'Имя не короче 2 символов!';
      }
      else {
        addApp( $name, $phone ); // Вместо отправки емаил отправляем данные куда либо в другое место: файл, БД, облако и т.п.
        $isSend = true;
      }
    }
    else {
      $name = '';
      $phone = '';
    }
    ?>

    <div class="form">
      <?php if( $isSend ): ?>
        <p>Your app is done!</p>
      <?php else: ?>
        <form method="post">
          Name:<br>
          <input type="text" name="name" value="<?=$name?>"><br>
          Phone:<br>
          <input type="text" name="phone" value="<?=$phone?>"><br>
          <button>Send</button>
          <p><?=$err?></p>
        </form>
      <?php endif; ?>
    </div>

## model/apps.php
Хранит в себе функции, две из них локальные, которые не вызываются из index.php.

    <?php
    // Функция возвращает массив с заявками
    // Получает информацию из файла db/apps.txt, файл можно назвать apps.json
    function getApps() : array {
      $str = file_get_contents( 'db/apps.txt' ); // Возвращает строку лежащую в apps.txt. Путь отчитывается от точки входа, index.php
      return json_decode( $str, true ); // Преобразовывает данные из формата JSON в PHP-объект или -массив (true)
    }

    // Получает массив в параметр и преобразует его в JSON код
    // JSON код вставляет в файл, добавляя его
    // Функция возвращает булев тип данных (удалось добавить заявку или нет)
    function saveApps( array $apps ) : bool {
      $str = json_encode( $apps ); // Преобразует массив в JSON
      file_put_contents( 'db/apps.txt', $str ); // Помещает JSON-строку в файл
      return true;
    }

    // Добавляем новую заявку
    function addApp( string $name, string $phone ) : bool {
      $dt = date( "Y-d-m H:i:s" );
      $app = [ 'dt' => $dt, 'name' => $name, 'phone' => $phone ]; // Собераем все полученные из формы данные в массив (одна заявка описывается одним ассоциативным массивом)
      $allApps = getApps(); // Получаем массив со всеми заявками
      $allApps[] = $app; // В полученный массив добавляем новую заявку (аналог array_push())
      return saveApps( $allApps ); // Сохраняем новый массив
    }

## admin.php
Просмотр информации в хранилище.

    <?php
    include_once('model/apps.php');
    $apps = getApps();
    ?>

    <table>
      <tr>
        <td>Date</td>
        <td>Name</td>
        <td>Phone</td>
      </tr>
      <?php foreach($apps as $app): ?>
      <tr>
        <td><?=$app['dt']?></td>
        <td><?=$app['name']?></td>
        <td><?=$app['phone']?></td>
      </tr>
      <?php endforeach; ?>
    </table>

## db/apps.txt
Внтури файла помещаем пустые кваратные скобки для JSON. Для работы с JSON в PHP есть две функции `json_encode()` и `json_decode()`.
