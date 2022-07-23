# Laravel

## Кэш

Очистка кэша конфигурационных файлов без последующего кэширования:
```
php artisan config:clear
```

Очистка кэша конфигурационных файлов с последующим кэшированием:
```
php artisan config:cache
```

## Миграции

Создать миграцию с указанием создания таблицы:
```
php artisan make:migration create_employees_table --create=employees
```

Запустить миграцию:
```
php artisan migrate
```

Откатить последнюю миграцию:
```
php artisan migrate:rollback --step=1
```

## Сидирование

Создать сидер:
```
php artisan make:seeder EmployeesTableSeeder
```

Заполнить БД с помощью указанного класса:
```
php artisan db:seed --class=EmployeesTableSeeder
```

## Классы

Composer psr-4 автолоадер:
https://laracasts.com/lessons/psr-4-autoloading

## Роутер

Вывести список API-роутов в консоли:
```
php artisan api:routes
```

## Логгинг

Подключить класс к файлу:
```
use Log;
```

Использование:
```
Log::info($data);
```

Отправить в FirePHP:
http://www.codediesel.com/php/debuggin-laravel-with-monolog-and-firephp/

Мой вариант:
```
$monolog = Log::getMonolog();
$monolog->setHandlers([new \Monolog\Handler\FirePHPHandler()]);
Log::info($data);
```

Конфигурируем лог один раз в `bootstrap\app.php`:
```
//my monolog configuration
$app->configureMonologUsing(function($monolog) {
    $monolog->setHandlers([new \Monolog\Handler\FirePHPHandler()]);
});
```
А потом используем лишь:
```
Log::info($data);
```