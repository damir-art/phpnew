# Циклы

## foreach
`foreach` - цикличный оператор.

Схема:

    foreach ($arr as $value) {
      echo $value;
    }

Вывод значений элементов массива:

    $person = [
      'name' => 'Ivan',
      'age' => 21,
      'hobby' => 'swimming',
      'is_married' => true,
      'pet' => 'cat',
      'pet_name' => 'Markiz',
      'pet_age' => 3
    ];

    foreach ($person as $value) {
      echo $value . '<br />';
    }

Вывод ключей и значений элементов массива:

    foreach ($person as $key => $value) {
      echo $key . ': ';
      echo $value . '<br />';
    }
