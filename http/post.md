# $_POST
Чтобы работать методом пост обязательно нужна форма

    <?php
      // узнаём какой метод отработал, если открывается страница то гет, если отправлена форма то пост
      echo $_SERVER['REQUEST_METHOD'];
      echo '<pre>';
      print_r($_POST);
      echo '</pre>';
    ?>

    <!--
      method по умолчанию равен гет
      если method у формы равен гет (форма поиска по сайту, фильтры), то значения name попадают в адресную строку
    -->
    <form method="post">
      <input type="text" name="a"><br />
      <input type="text" name="b"><br />
      <button>Send</button> <!-- по умолчанию тип сабмит -->
    </form>

см пример по сложнее в `example/form.md`
