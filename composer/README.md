# Composer
Composer – это инструмент управления зависимостями для PHP-проектов. Он помогает разработчикам легко управлять библиотеками и другими внешними компонентами, необходимыми для работы приложения. С помощью Composer можно автоматизировать установку, обновление и удаление пакетов, а также контролировать их совместимость между собой.

## Установка Composer
Для начала нужно скачать и установить сам Composer:
1. Перейти на официальный сайт Composer (https://getcomposer.org/download/).
2. Скачать установочный скрипт.
3. Запустить команду в консоли для глобальной установки:
```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c032046d1ce885912de02751') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

Теперь у вас установлен Composer, и он доступен глобально. Вы можете проверить успешность установки командой:
```bash
composer --version
```

## Использование Composer

### Создание файла `composer.json`
Файл `composer.json` содержит информацию о зависимостях вашего проекта. Чтобы создать этот файл, выполните следующую команду в папке вашего проекта:

```bash
composer init
```

Вам будет предложено ввести некоторые данные о вашем проекте, такие как имя, описание, автор и т.д. Также вы сможете добавить начальные зависимости прямо при создании файла.

Пример простого `composer.json`:

```json
{
  "require": {
    "monolog/monolog": "^2.0",
    "guzzlehttp/guzzle": "~7.0"
  }
}
```

Здесь мы указали две зависимости: `monolog/monolog` и `guzzlehttp/guzzle`. Первая версия должна быть **не ниже** 2.0, вторая – примерно 7.0 (то есть могут быть установлены любые патчи этой версии, но не мажорные изменения).

### Установка зависимостей
Чтобы установить указанные в `composer.json` зависимости, выполните команду:

```bash
composer install
```

Эта команда создаст папку `vendor`, куда будут помещены все установленные библиотеки, и файл `composer.lock`, содержащий точные версии всех установленных пакетов. Этот файл используется для того, чтобы другие разработчики могли получить точно такую же версию зависимостей, какую используете вы.

### Обновление зависимостей
Когда выходят новые версии ваших зависимостей, вы можете обновить их с помощью команды:

```bash
composer update
```

Эта команда обновляет все зависимости до последних допустимых версий согласно вашим требованиям в `composer.json`.

### Добавление новой зависимости
Чтобы добавить новую зависимость к вашему проекту, выполните команду:

```bash
composer require vendor/package
```

Например:

```bash
composer require symfony/http-foundation
```

Эта команда добавит зависимость от пакета `symfony/http-foundation` в ваш `composer.json` и сразу установит её.

## Заключение
Composer значительно упрощает работу с зависимостями в PHP-проектах, позволяя автоматически управлять установкой, обновлением и удалением внешних библиотек. Он стал стандартным инструментом для большинства современных PHP-разработчиков.
