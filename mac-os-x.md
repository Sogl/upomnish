# Mac OS X

## Общее

Понять что заняло 80-й порт:
```
sudo lsof -i -n -P | grep TCP
```

## brew

Установка с отключением автообновления:
```
HOMEBREW_NO_AUTO_UPDATE=1 brew install <formula>
```

Более подробно: https://computingforgeeks.com/prevent-homebrew-auto-update-on-macos/

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

## Spotlight

Если достал при загрузке процесс mds_stores, следующая команда позволит увидеть чем он вообще в файловой системе занимается:
```
sudo fs_usage -w -f filesys mdworker_shared
```
Ненужные для индексации папки потом можно упрятать в исключения в настройках.

Связанные ссылки:
https://apple.stackexchange.com/questions/144474/mds-and-mds-stores-constantly-consuming-cpu
https://apple.stackexchange.com/questions/162227/how-to-isolate-processes-that-evoke-insane-mds-stores-disk-read-activity
https://medium.com/devops-one-problem-at-a-time/curing-macs-high-cpu-fan-noise-heat-6b567cb81ea0
https://wiert.me/2021/04/19/spotlight-taking-200-cpu/

Интересный сайт с разными нюансами (и софтом) для мака:
https://eclecticlight.co/
