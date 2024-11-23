# image
Загружаем изображения на сервер, создаём фотогалерею. Сканируем директорию, фильтруем в ней файлы (изображения).

- index.php - выводит галерею
- admin.php - загружает изображение
- model/gallery.php
- images/

Без БД галерея не может быть полноценной, потому что нельзя их отсортировать.  
При загрузке файла на сервер, важно контролировать расширение, размер файла, дать ему новое имя и заного его пересоздать через imagecreatefromjpeg() и пересохранить.

## index.php

```php
declare( strict_types=1 );
include_once( 'model/gallery.php' );

// Получаем список изображений
$files = scandir( 'images' ); // сканируем папку images, возвращаем список файлов которые в ней есть

// echo '<pre>';
// print_r( $files ); // массив с именами файлов, . - ссылка на текущую директорию, .. - ссылка на родительскую
// echo '</pre>';

// Фильтруем элементы массива, они должны быть файлом и иметь расширение .jpg
// Если array_filter() добавить третий параметр, то он также будет убирать ключи, превращая ассоциативный массив в обычный
$images = array_filter( $files, function( $f ) {
  return is_file( "images/$f" ) && checkImageName( $f ); // возвращает false для тех элементов которые должны быть удалены из массива
});

/*
* Аналог с циклом, фильтра выше
$images = [];
foreach( $files as $f ) {
  if( is_file( "images/$f" ) && preg_match( '/.*\.jpg$/', $f ) ) {
    $images[] = $f;
  }
}
*/
```

```html
<!-- Выводим изображения из отфильтрованного массива -->
<div class="gallery">
  <?php foreach( $images as $img ) : ?>
  <img src="images/<?=$img?>" alt="" width="100">
  <?php endforeach; ?>
</div>
```

## admin.php

```php
declare(strict_types=1);
include_once('model/gallery.php');

/**
 * Загружаем изображения на сервер
 * Чтобы вам не закинули на сервер экзешник чье расширение поменяли на jpg или png,
 * нужно чтобы сервер при загрузке изображения заного его пересоздавал
 */

$isSend = false;
$err = '';

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  // Форма отрпавляется методом пост, но при загрузке изображения она всё равно пуста
  // потому что информация о файле попадает в массив $_FILES
  // echo '<pre>';
  // print_r( $_POST );
  // print_r( $_FILES ); // чтобы не было ерора, файл должен соответсвовать настройкам в PHP.ini по размеру и количеству загружаемых изображений
  // echo '</pre>';

  $file = $_FILES['file']; // присваиваем переменной, загружаемый файл

  // По этому файлу проверяем на различные соответствия
  if ( $file['name'] === '' ) {
    $err = 'Файл не выбран!'; // если форма отправляется без файла
  }
  // || filesize($file['tmp_name']) > 1024 * 1024 * 2 // или размер больше необходимого
  else if ( $file['size'] === 0 ) {
    $err = 'Файл слишком большой!'; // если имя на сервер пришло, а размер равен 0, то значит он слишком большой и не попал во временную папку tmp
  }
  // Проверяем является ли окончание файла .jpg
  // составляем белый список, то что разрешено
  else if( !checkImageName( $file['name'] ) ) {
    $err = 'Только jpg';
  }
  else {
    // Если все проверки пройдены, заного пересоздаём изображение и копируем его из папки тмп в нужную
    // сами создаём новое имя файл через рандом, для безопасности
    // echo '<pre>';
    // print_r( $_FILES );
    // echo '</pre>';
    copy( $file[ 'tmp_name' ], 'images/' . mt_rand( 1000, 100000 ) . '.jpg' );
    $isSend = true;
  }
}
?>
```

```html
<div class="form">
  <?php if ( $isSend ) : ?>
    <p>Your image is done!</p>
  <?php else: ?>
    <form method="post" enctype="multipart/form-data">
      <input type="file" name="file">
      <button>Send</button>
      <p><?=$err?></p>
    </form>
  <?php endif; ?>
</div>
```

## model/gallery.php

```php
declare( strict_types=1 );

// Проверяет есть ли у файла расширение .jpg
function checkImageName( string $name ) : bool {
  return !!preg_match( '/.*\.jpg$/', $name );
}
```