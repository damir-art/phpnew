# Многомерный массив

    $persons = [
      $person0 = [
        'name' => 'Ivan',
        'age' => 21,
        'hobby' => 'swimming',
        'is_married' => true,
        'pet' => 'cat',
        'pet_name' => 'Markiz',
        'pet_age' => 3,
        'cars' => [ 'bmw', 'audi', 'volvo' ]
      ],
      $person1 = [
        'name' => 'Petr',
        'age' => 23,
        'hobby' => 'swimming',
        'is_married' => false,
        'pet' => 'cat',
        'pet_name' => 'Markiz',
        'pet_age' => 3
      ],
      $person2 = [
        'name' => 'Sidor',
        'age' => 25,
        'hobby' => 'swimming',
        'is_married' => true,
        'pet' => 'cat',
        'pet_name' => 'Markiz',
        'pet_age' => 3
      ]
    ];

Выводим все имена:

    foreach ($persons as $arr) {
      echo $arr['name'] . '<br />';
    }

Выводим значения всех элементов у массивов:

    foreach ($persons as $arr) {
      foreach ($arr as $item) {
        echo $item . '<br />';
      }
    }

Если у person `'is_married' => true,`, выводим его имя:

    foreach ($persons as $arr) {
      if ($arr['is_married']) {
        echo $arr['name'] . '<br />';
      }
    }
