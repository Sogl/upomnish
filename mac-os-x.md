# Mac OS X

## Общее

Понять что заняло 80-й порт:
```
sudo lsof -i -n -P | grep TCP
```

## DNS

Очистить кэш:
```
sudo dscacheutil -flushcache
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

# Network

Узнать IP домена:

1) Так:
```
dig +short example.com
```
2) Или так:
```
host example.com
```
3) Или так:
```
nslookup example.com
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

С портом и ssh-ключом:
```
ssh user@host -p port -i ~/.ssh/key
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

## Документы

Сконвертировать .docx в markdown (с выгрузкой изображений в папку `media`, формат GithubFlavouredMarkdown, без разрывов строк):
```
pandoc -f docx -t markdown foo.docx -o foo.md --extract-media=./ -t gfm --wrap=none
```
Предварительно нужно установить pandoc `brew install pandoc`


## Снять атрибут карантина

Помогает для VST что нельзя снять через системные настройки (r — рекурсивно):
```
sudo xattr -rd com.apple.quarantine LOADED.vst3
```

## Xdebug

Настройка: https://javorszky.co.uk/2018/05/03/getting-xdebug-working-on-php-7-2-and-homebrew/
