# Создание чата
Создание чата с использованием PDO. Чот это тот же блог только упрощенный.

- создаём БД `php1simple`
- создаём таблицу `messages`
- Поля:
  - id_message: INT, UNSIGNED, PRIMARY, A_i
  - name: VARCHAR, 128
  - text: TEXT
  - dt_add: TIMESTAMP, CURRENT_TIMESTAMP
- Сохранить

## Подключение к БД
```php
// Создаём экземпляр класса PDO
// Конструктор класс PDO принимает минимум три параметра
// 1. Куда подключаемся, 2. Имя пользователя, 3. Пароль
// Если открыть страницу и не будет ошибок, то значит успешно подключились к БД
$db = new PDO('mysql:host=localhost;dbname=php1simple','root','');
// Если возникают проблемы с кириллицей
// $db->exec('SET NAMES UTF8');

// exec() - запуск одной произвольной команды, SQL-запроса
// Добавляем в таблицу messages в поля name и text, значения
$sql = "insert messages (name, text) values ('user', 'Привет')";
$db->exec($sql);
```

## Разное
Если возникает проблема с кириллицей, то можно добавить в настройки `charset=utf8`:

```
mysql:host=localhost;dbname=php1simple;charset=utf8
```

или сразу после подключения БД, прописать строку:

```php
$db->exec('SET NAMES UTF8');
```