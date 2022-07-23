# Mac OS X

## Общее

Понять что заняло 80-й порт:
```
sudo lsof -i -n -P | grep TCP
```


## MySQL

Версия 5.7.
Остановка:
```
sudo launchctl unload /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist
```

Запуск:
```
sudo launchctl load -F /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist
```

Конфиг класть сюда:
```
/usr/local/mysql/etc/my.cnf
```
Начальный лежит здесь:
```
/usr/local/mysql/support-files/my-default.cnf
```

## Apache

Запуск от имени текущего пользователя.
Конфигурация тут:
```
/private/etc/apache2/httpd.conf
```
Пишем это:
```
User %username%
Group staff
```

https://apple.stackexchange.com/a/46219

## Терминал

Запуск ssh-сессии:
```
ssh root@IPaddress
```

Обновление PATH переменных:
```
source ~/.bashrc
```

## Composer

Установка глобально:
```
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

# Документы

Сконвертировать .docx в markdown с выгрузкой изображений (формат GithubFlavouredMarkdown):
```
pandoc -f docx -t markdown foo.docx -o foo.md --extract-media=./ -t gfm --wrap=none
```
Предварительно нужно установить pandoc `brew install pandoc`

