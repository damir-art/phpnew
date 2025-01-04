# fopen big
Читаем большой файл по частям. Если его попытаться прочитать с помощью метода file(), он выдаст ошибку и будет напрягать оперативку.

```php
/* 
* Создадим файл из 2х млн строк

$f = fopen('db.txt', 'w');

for($i = 0; $i < 2000000; $i++){
  fwrite($f, mt_rand(1000000, 10000000) . "\n");
}

fclose($f);
*/

/*
* Выясним сколько памяти нужно чтобы прочитать этот файл
$a = file('db.txt');
echo memory_get_usage(); // 116 042 528
*/

/*
* Вычислим среднее значение суммы всех рандомных чисел в файле db.txt
* благодаря fopen() это вычесление займет не более 1 мб памяти
*/
$f = fopen('db.txt', 'r');
$total = 0;
$cnt = 0;

// fgets читает строки до того момента пока не встретит перенос строки
while(!feof($f)){
  $str = rtrim(fgets($f));

  if($str !== ''){
    $total += $str;
    $cnt++;
  }
}

echo memory_get_usage() . '<br />'; // 401 424
echo $total / $cnt;
fclose($f);
```