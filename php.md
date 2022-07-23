# PHP

Узнать версию php:
```
php -v
```

Информация о php в консоли (с выводом в файл):
```
echo "<?php phpinfo(); ?>" | php > /tmp/phpinfo.txt`
```

## Часовой пояс (например, UTC +11)

Таймзона web:
```
/etc/php5/apache2/php.ini
```
Таймзона cli:
```
/etc/php5/cli/php.ini
```
Для web, cli:
```
date.timezone = "Etc/GMT-11"
```
Для .htaccess:
```
php_value date.timezone Etc/GMT-11
```

## Xdebug

Статья про PHPStorm: https://blog.denisbondar.com/post/phpstorm_docker_xdebug
Мои мучения с ним: https://github.com/laradock/laradock/issues/2848

Поможет в docker узнать сетевой адрес:
```
docker network inspect bridge | grep Gateway
```

Параметры xdebug.ini в Laradock под MacOSX:
```ini
; NOTE: The actual debug.so extention is NOT SET HERE but rather (/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini)

xdebug.remote_host="host.docker.internal"
xdebug.remote_connect_back=0
xdebug.remote_port=9000
xdebug.idekey=PHPSTORM

xdebug.remote_autostart=1
xdebug.remote_enable=1
xdebug.cli_color=0
xdebug.profiler_enable=0
xdebug.profiler_output_dir="~/xdebug/phpstorm/tmp/profiling"
; my addition for logs
xdebug.remote_log=/tmp/xdebug_remote.log

xdebug.remote_handler=dbgp
xdebug.remote_mode=req

xdebug.var_display_max_children=-1
xdebug.var_display_max_data=-1
xdebug.var_display_max_depth=-1
```

Параметры в xdebug.conf (или php.ini)   [старые]:
```
zend_extension=xdebug.so
xdebug.remote_host = 127.0.0.1
xdebug.default_enable = 1
xdebug.idekey = "atom-xdebug"
xdebug.remote_enable = 1
xdebug.remote_port = 10000
xdebug.extended_info = 1
xdebug.remote_handler = "dbgp"
xdebug.remote_mode = "req"
xdebug.remote_connect_back = 1
;куда писать логи
;xdebug.remote_log="/tmp/xdebug.log"

xdebug.auto_trace = 0
xdebug.collect_includes = 1
xdebug.dump.REQUEST = *
xdebug.dump.SESSION = *
xdebug.dump.SERVER = REMOTE_ADDR,REQUEST_METHOD
xdebug.dump_globals = 1
xdebug.dump_once = 1
xdebug.dump_undefined = 1
xdebug.max_nesting_level = 256
xdebug.overload_var_dump = 1
xdebug.profiler_enable = 0
xdebug.profiler_enable_trigger = 1
```


Отладка консольного php-файла:
```
XDEBUG_CONFIG=”idekey=atom-xdebug” php /usr/share/glpi/front/cron.php
```

## APC

APC кеш в php.ini:
```
[APC]
extension=apc.so
apc.shm_size = 128M
apc.enable_cli = on
apc.cache_by_default = on
apc.user_ttl = 60
apc.slam_defense = 0
apc.write_lock = 1
```

Моя конфигурация:
```
[APC]
extension=apcu.so
apc.enabled=1
apc.shm_size=128M
apc.enable_cli=1
apc.cache_by_default = 1
apc.user_ttl = 60
apc.slam_defense = 0
apc.write_lock = 1
apc.ttl=7200
apc.gc_ttl=3600
```