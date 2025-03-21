# Code style
Код-стайл (code style) - набор правил и соглашений для написания кода, над которым работает более одного разработчика.

- имена переменных/функций должны быть говорящими и записываться кэмэл кэйсом,
- функции должны быть глаголом, начинаться со слова действия get/set/add/check и т.п,
- функции нужно параметризировать (делать больше параметров, делать универсальной), чтобы функции были как можно меньше завязаны на глобальные данные, массивы,
- плохая функция сама решает откуда берет данные и сбор данных находится внутри этой функции,
- хорошая функция принимает данные с которыми она работает, а не получает их внутри себя,
- старайтесь внутри функции не обращаться к глобальным предопределённым массивам,
- с глобальными предопределёнными массивами должен работать файл который запускается напрямую, например index.php,
- объявлять функцию внутри index.php не рекомендуется, для функций нужно создать отдельный файл, чтобы к ним можно было обратиться из любого файла приложения,
- `include_once('functions.php')` подключаем файл с функциями,
- функции нужно не только параметризировать но и делать им строгую типизацию (помогает делать код однозначным, не допускает ситуации кода функции возвращает либо строку либо число, что приводит к путаннице в коде),

Пример кода `index.php`:

    // Включаем строгую типизацию (это нужно размещать в каждом файле, где вызывается функция, если проверяем переданные аргументы и там где функция объявляется, если проверяем возвращаемое значение)
    // Без этой строки не будет строгой типизации, а будет автоматическое приведение типов
    declare(strict_types=1);

    include_once('functions.php'); // подключаем файл functions.php

    $articleId = 1; // camel case
    // checkId($_GET['id']); // функция которая передает данные, обращаться к $_GET['id'] внутри функции, не рекомендуется
    // checkId($_GET['id'] ?? ''); // чтобы не было предупреждений об ошибках, используйте ??
    // checkId("12"); // передаём другие данные, функция универсальная
    // checkId(12); // если передать число то появится ошибка, о том что переданное значение должно быть строкой

    var_dump(checkId($_GET['id'] ?? ''));
    // var_dump(checkId(12));

`functions.php` файлы где хранятся функции, для каждой функции рекомендуется создавать отдельный файл:

    declare(strict_types=1);

    function getArticle(){

    }

    // Строга типизация в PHP, функция принимает строку и возвращает булевый тип данных
    function checkId(string $id) : bool {
      return ctype_digit($id); // функция проверяет состоит ли строка только из цифр
    }
