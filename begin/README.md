# Основы
Основы работы с PHP

Весь код помещаем между:

    <?php
      // код
    ?>

## Вывод
Любое выражение можно вывести с помощью конструкции вывода `echo`.

    echo 'Hello'; // инструкция
    echo 2 * 2;

После каждой инструкции ставится точка с запятой.  
Любой текст это уже программа на PHP.  
Вывод встраивается в страницу и уже в готовом виде отправляется клиенту.  
Клиенту передаётся результат выполнения программы.  
Текст и HTML-код выводится, всё что между `<?php  ?>` выполняется и вставляется в вывод (stdout).  
stdout - поток вывода.

## Присваивание

    $x = 2; // создаём значение 2 и даём этому значению имя x
    2; // можно просто записать 2, но так как это значение нигде не присвоено, то оно в коде программы участвовать не будет

## Выражение, значение
Выражение - это некое значение, заданное или в явном виде (литерал) или в виде некоего вычисления (последовательности операций). У каждого выражения есть своё значение, чему оно равно.

- 2 - число (выражение задано явно) (int)
- 1.5 - число (float)
- 'text' - строка (string)
- 2 + 2 - выражение, значение равно 4

Выражение всегда имеет значение (то чему оно равно).  
Присваивание тоже является выражением: `$a = 1;`, его значением будет то что присвоено.  

В PHP всё является выражением. Выражение это нечто что имеет значение и может быть присвоено в переменную. То что можно вычислить и присвоить в переменную.

    $x = 2 + 2;
    2 + 2 // выражение
    4 // значение выражения

    $x = ($y = 4);
    $x = $y = 5; // так тоже сработает
    ($y = 4) // выражение

Значением присваивания как опреации является то что присвоено.

    echo $x = 3; // 3

## Операция
- арифметическая - ( + - * / % )
- сравнение - ( == != < > >= <=)
- логическая - ( && || ! )
- строковая - конкатенация `.`
- остальные

% - остаток, сравнение по модулю.

Приоритет операций:

    // Сначала выполнится операция в скобках
    echo ($a = 4) * 2; // 8
    echo $a; // 4

    // Результат без скобок
    echo $a = 4 * 2; // 8
    echo $a; // 8

    // Операция присваивания приоритетней чем xor
    var_dump( true xor true ); // false
    echo $a = true xor true;
    var_dump($a); // true

    // Так правильней
    echo $a = (true xor true); // false

`$a = true xor true` - первое `true` присвоется переменной `a`, далее операция `$a xor true`, чьим значением будет `false`, никуда не присвоится.

## Переменная
Переменная - это значение (выражение), сохраненное под каким-либо именем. Значение хранится в памяти.

Пример:

    $email = 'test@example.com';
    $age = 24;
    $result = 1 + 2 * 3;

Имя переменной в PHP начинается со знака `$`. Обратите внимание, что `$a` и `$A` - это разные переменные!
В PHP объявление переменной (создание имени) и присваивание ей значения - это одна операция. Можно объявить переменную, без значения:

    $a;

В этом случае переменная имеет значение `null`.  
Имена переменных латинскими, с маленькой буквы, кемел кейс.  

## Тип переменной
В PHP тип имеют значения, а не переменные. Переменная - это просто имя для значения, чтобы его сохранить на будущее.

- `int`, `integer` - целые числа. Любые. Включая, конечно, ноль. Замкнуты относительно сложения, вычитания, умножения - результат снова будет целым числом. А вот при делении - не факт!
- `float`, `double` - Тоже числа. Но не целые, а имеющие дробную часть. Иногда нулевую, но всё равно имеющие. Являются приближенными (не точными). Легко получить, написав число с десятичной точкой, или используя операции, дающие не целый результат (деление, как пример).
- `string` - Строки. Последовательность байт. То, что состоит из символов. В PHP строки:
  - Могут быть любой длины (хоть вся "Война и мир"), главное поместиться в доступной памяти,
  - Могут быть нулевой длины (пустые), `$str = '';`
  - Могут заключаться в одинарные или двойные кавычки. Это почти одно и тоже.
    - $str1 = 'test'; - одинарные кавычки рекомендуется.
    - $str2 = "test";
    - но:
    - $foo = 'Hello\n';
    - $bar = "Hello\n";
- `boolean (bool)` - логическое значение `true` или `false`.
  - в PHP это не ноль и не единица
  - при echo преобразуется к строке: true - 1, false - не выводится (пустая строка)
  - равенство записывать знаком `==`
  - выражение дающие логический результат: `$a = $b > $c;`
  - используйте логические операторы `&&`, `||`, не пишите словами `or`
  - в операторах сравнения и логических желательно использовать скобки
  - чаще всего используются в управляющих конструкциях: операторы ветвления, циклы

PHP_INT_MAX - дать максимальное число.  
float в арифметических операциях могут терять точность `(0.1 + 0.2) == 0.3`. Максимальная точность 15 цифр.  
Строки в PHP считаются побайтово, например строка записанная кириллицей будет иметь размер х2 байт (в UTF-8 кириллица кодируется двумя байтами).  
Любая не пустая строка равна `true`.  
При вычислении условия, желательно записываться так: `значение == $a`, а не `$a == значение` чтобы при ошибочной записи `=` вместо `==`, появилась ошибка.  

## Приведение типов
Тип результата операции всегда определятеся оператором:
- аримфетические операции создают числа
- конкатенация создаёт строку
