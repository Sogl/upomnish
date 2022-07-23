# Linux

Все актуально для Ubuntu Linux

## Git

Установка последней версии:
```
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

## Apache

Узнать версию apache:
```
apache2ctl -v
```
модули апача установленные:
```
apache2ctl -M
```

Сменить модуль php (в случае перехода с 5.5 на 5.6):
```
sudo a2dismod php5 && sudo a2enmod php5.6 && sudo service apache2 restart
```


## MySQL

Узнать версию mysql:
```
mysql -h localhost -V
mysql --version
```

Посмотреть список активных процессов-соединений:
```
show full processlist;
```

Добавить нового пользователя с доступом из локальной подсети:
```
grant all privileges on *.* to 'root'@'192.168.%' with grant option;
flush privileges;
```

Уменьшить размер таблицы:
```
OPTIMIZE TABLE table_name;
```

Моя конфигурация версии 5.7:
```
[mysqld]

#MEZ
#--no password expiration--
default_password_lifetime=0

#--collation--
init_connect='SET NAMES utf8'
character-set-server = utf8
collation-server = utf8_general_ci

#--innodb settings--
default-storage-engine = INNODB
innodb_buffer_pool_size = 4G
innodb_log_file_size = 2G
innodb_file_per_table = ON
innodb_flush_log_at_trx_commit = 2
innodb_flush_method = O_DIRECT
sync_binlog = 0

#--other--
max_connections = 1000
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

#--logs--
#log binary
server_id = 0
log_bin = /var/log/mysql/mysql-bin
max_binlog_size = 500M
expire_logs_days = 3
#log error (start messages)
log-error = /var/log/mysql/mysql-error.log
log_error_verbosity = 2
#log slow queries
slow-query-log = 1
slow-query-log-file = /var/log/mysql/mysql-slow.log
long_query_time = 3
#query general log
#general_log = 1
#general_log_file = /var/log/mysql/mysql-query.log
#log_output = TABLE
#/MEZ
```

## Percona xtrabackup

Бекап:
```
innobackupex --defaults-file=/etc/mysql/my.cnf --no-timestamp --user=root --password="$(cat /root/.mysql)" --databases="puls" /mnt/backup/mysql/puls
```
Бекап бинарных логов:
```
/usr/local/xtrabackup/bin/innobackupex --apply-log --redo-only --defaults-file=/etc/my.cnf --password="$(cat /root/.mysql)" --no-timestamp  --throttle=40
```


## Каталоги и файлы

Для вновь скопированных файлов в папку сервера (с записью для группы):
```
chmod -R 0775 /var/www
chown -R root:www-data /var/www
```
Права 644 только для файлов:
```
find /var/www -type f -exec chmod 644 {} +
```

Размер текущей папки:
```
du -sh
```

## Пользователи и группы

Создание пользователя с домашним каталогом:

1. В группе users:
```
useradd -g users -G adm,sudo,www-data -s /bin/bash -m -d /home/user user
```
2. Со своей группой:
```
useradd -G adm,sudo,www-data -s /bin/bash -m -d /home/user user
```

Переименовать юзера (только от другого!):
```
usermod --move-home --login newusername --home /home/newusername oldusername
```

Отобразить список всех пользователей:
```
cut -d: -f1 /etc/passwd
```

Отобразить список всех групп:
```
getent group
```

Получить gid группы (вместо `users` можно вписать `group id`):
```
getent group users
```

## CRON

Редактировать текущие задания:
```
crontab -e
```

Папка root:
```
/var/spool/cron/crontabs
```
Папка куда можно кидать свои:
```
/etc/cron.d/
```

Просмотреть логи Crontab в реальном времени:
```
tail -f /var/log/syslog | grep CRON
```

После изменений не забыть перезапустить службу:
```
service cron restart
```

## Logrotate

Сохранение логов в течение 7 дней в формате `год-месяц-день`:
```
/var/log/puls/cron_notifications.log {
        daily
        missingok
        rotate 7
        #nocreate
        dateext
        dateyesterday
        dateformat .%Y-%m-%d
        extension .log
}

/var/log/puls/cron_clean_uploads.log {
        daily
        missingok
        rotate 7
        #nocreate
        dateext
        dateyesterday
        dateformat .%Y-%m-%d
        extension .log
}
```

## Сеть

Записать pcap файл для определенного порта и хоста (можно открыть в Wireshark):
```
tcpdump -i any -vvv 'host host.server.com' -s0 -w /tmp/server.pcap
```

Узнать кто занял 80 порт:
```
sudo update-rc.d -f nginx disable
```

Просмотреть открытые порты:
```
netstat -tnlp
```

## Монтирование дисков и директорий (NFS)

Вики: [http://help.ubuntu.ru/wiki/nfs](http://help.ubuntu.ru/wiki/nfs)

1. **Сервер.** Строка в `/etc/exports`:
```
"/backup" *(insecure,insecure_locks,rw,sync,no_subtree_check) 192.168.1.226(rw,no_subtree_check,insecure,insecure_locks,sync,all_squash,anonuid=98,anongid=101)
```
Перезалив конфигурации:
```
exportfs -a
```
2. **Клиент.** Смонтировать NFS:
```
mount -t nfs -O iocharset=utf-8 nas:/backup /mnt/backup
```
Размонтировать:
```
umount /mnt/backup
```
Добавляем в fstab:
```
nas:/backup /mnt/backup nfs defaults 0 0
```