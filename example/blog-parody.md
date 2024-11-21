# Пародия на блог
Пародия на блог в качестве хранилища данных выступает массив.

## index.php

    <?php
      // Подключаем файл с функциями
      include_once('functions.php');
      $articles = getArticles(); // получаем многомерный ассоциативный массив (типа JSON) из функции
      // print_r( $articles );
    ?>

    <div class="articles">
      <?php
        foreach ($articles as $id => $article): ?>
          <div class="article">
            <!-- id это ключ массива, внутри массива есть еще элемент с ключем id -->
            <h2><?php echo $article['title']; ?></h2>
            <!-- <a href="article.php?id=<?php echo $article['id']; ?>">Read more</a> -->
            <a href="article.php?id=<?php echo $id; ?>">Read more</a>
          </div>
      <?php
        endforeach;
      ?>
    </div> <!-- articles -->

## functions.php

    function print_pre($a) {
      echo '<pre>';
      print_r($a);
      echo '</pre>';
    }

    // Функция обращающаяся к хранилищу данных, возвращает массив
    function getArticles() {
      return [
        '1' => [
          'id' => 1,
          'title' => 'Заголовок 1',
          'content' => 'Описание страницы с id = 1.'
        ],
        '2' => [
          'id' => 2,
          'title' => 'Заголовок 2',
          'content' => 'Описание страницы с id = 2.'
        ],
        '5' => [
          'id' => 5,
          'title' => 'Заголовок 5',
          'content' => 'Описание страницы с id = 5.'
        ]
      ];
    }

## article.php

    <?php
      include_once('functions.php');
      $articles = getArticles();

      // print_pre($articles);

      $id = (int)($_GET['id'] ?? ''); // получаем гет параметр id
      $post = $articles[$id] ?? null; // получаем статью по его id
      $hasPost = ($post !== null);    // проверяем наличие статьи

    ?>

    <!-- Вывод статьи -->
    <div class="content">
      <?php if($hasPost): ?>
        <div class="article">
          <h1><?=$post['title']?></h1>
          <div>
            <?=$post['content']?>
          </div>
          <p>
            <a href="/php/">На главную</a>
          </p>
        </div>
      <?php else: ?>
        <div class="e404">
          <h1>Страница не найдена!</h1>
        </div>
      <?php endif; ?>
    </div>
