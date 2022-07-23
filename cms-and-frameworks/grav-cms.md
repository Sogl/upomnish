# Grav CMS

## Composer

Установить все пакеты composer для всех плагинов:
```
find . ./user/plugins/ -name composer.json -maxdepth 2 -execdir composer install \;
```