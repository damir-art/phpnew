# Основы SQL
Список простых и популярных SQL-запросов с кратким описанием.
- выборка (select), условия, группировки, многотабличные запросы

Эти пишутся одной командой.
- добавление (insert)
- удаление (delete)
- редактирование (update)

В запросах UPDATE и DELETE используем WHERE

Переходим:
- phpMyAdmin > php1 (БД) > shops (таблица)
- внизу жмем по кнопке INSERT (появится шаблон команды)

Для наглядности команды запроса напишем в отдельных строках:

```sql
INSERT INTO `shops`
(`id_shop`, `title`, `site`, `address`)
VALUES
('[value-1]','[value-2]','[value-3]','[value-4]')
```

- INSERT INTO `shops` - вставить в "Название таблицы"
- (`id_shop`, `title`, `site`, `address`) - в какие столбцы вставляем (необязательно перечислять все столбцы)
- VALUES - значения
- ('[value-1]','[value-2]','[value-3]','[value-4]') - какие значение вставляем в столбцы

```sql
INSERT INTO `shops`
(`title`, `site`)
VALUES
('Техносила','tehnosila.ru')
```

- старайтесь все значения обрамлять кавычками, даже числа и даты, кроме функций или вычислений
- названия таблиц столбцов можно не обрамлять обратными кавычками (бэктики), обрамлять обязательно только зарезервированные слова

## DELETE
```sql
DELETE FROM `departaments` WHERE id_dep = 4
```

- если повторить запрос удаления, он сработает, но удалит 0 строк
- WHERE - ставится в таких командах как DELETE, UPDATE, SELECT и определяет для какой строки мы совершаем операцию

## UPDATE
Обновляем поле дескриптион.

```sql
UPDATE products
SET
description = 'Скоро в продаже!'
WHERE
id_product = 2
```

Обновляем сразу два поля:
```sql
UPDATE products
SET
title = 'iPhone 2X',
description = 'Скоро в продаже!'
WHERE
id_product = 2
```

## Создание таблицы
```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  age INT
);
```
Создает новую таблицу `users` с тремя столбцами: `id` (первичный ключ), `name` и `age`.

## Добавление записи в таблицу
```sql
INSERT INTO users (name, age) VALUES ('Иван', 30);
```
Вставляет новую запись в таблицу `users` с именем 'Иван' и возрастом 30 лет.

## Выбор всех записей из таблицы
```sql
SELECT * FROM users;
```
Выбирает все записи из таблицы `users`.

## Выбор конкретных столбцов
```sql
SELECT name, age FROM users;
```
Выбирает только столбцы `name` и `age` из таблицы `users`.

## Фильтрация записей по условию
```sql
SELECT * FROM users WHERE age > 25;
```
Выбирает все записи из таблицы `users`, где возраст больше 25 лет.

## Сортировка результатов
```sql
SELECT * FROM users ORDER BY age DESC;
```
Выбирает все записи из таблицы `users` и сортирует их по возрасту в порядке убывания.

## Ограничение количества результатов
```sql
SELECT * FROM users LIMIT 5;
```
Выбирает первые пять записей из таблицы `users`.

## Объединение таблиц (JOIN)
```sql
SELECT users.name, orders.order_date
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```
Объединяет таблицы `users` и `orders` по полю `id` в таблице `users` и полю `user_id` в таблице `orders`, выбирая имя пользователя и дату заказа.

## Группировка данных
```sql
SELECT age, COUNT(*) AS count
FROM users
GROUP BY age;
```
Группирует записи по возрасту и считает количество записей в каждой возрастной группе.

## Агрегационные функции
```sql
SELECT AVG(age) AS average_age FROM users;
```
Вычисляет среднее значение возраста для всех записей в таблице `users`.

## Подсчет количества записей
```sql
SELECT COUNT(*) FROM users;
```
Подсчитывает общее количество записей в таблице `users`.

## Обновление записи
```sql
UPDATE users SET age = 35 WHERE id = 1;
```
Обновляет возраст на 35 для записи с `id` равным 1.

## Удаление записи
```sql
DELETE FROM users WHERE id = 2;
```
Удаляет запись с `id` равным 2 из таблицы `users`.

## Выбор уникальных значений
```sql
SELECT DISTINCT age FROM users;
```
Выбирает уникальные значения возраста из таблицы `users`.

## Создание индекса
```sql
CREATE INDEX idx_name ON users(name);
```
Создает индекс для столбца `name` в таблице `users`, что улучшает производительность поиска по этому столбцу.

## Изменение структуры таблицы
```sql
ALTER TABLE users ADD COLUMN address VARCHAR(255);
```
Добавляет новый столбец `address` в таблицу `users`.

## Удаление таблицы
```sql
DROP TABLE users;
```
Удаляет таблицу `users` из базы данных.

## Создание временной таблицы
```sql
CREATE TEMPORARY TABLE temp_users SELECT * FROM users;
```
Создает временную таблицу `temp_users`, копируя все данные из таблицы `users`.

## Транзакции
```sql
START TRANSACTION;
INSERT INTO users (name, age) VALUES ('Анна', 28);
COMMIT;
```
Начинает транзакцию, добавляет новую запись в таблицу `users` и завершает транзакцию.

## Резервное копирование базы данных
```bash
mysqldump -u root -p database_name > backup.sql
```
Создает резервную копию базы данных `database_name` в файл `backup.sql`.

Эти запросы охватывают большинство базовых операций, выполняемых в SQL, и помогут вам начать работать с базами данных.
