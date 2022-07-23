# git

## SSH-ключ для деплоя

**SSH ключ** чтобы работал для клонирования репозитория на Bitbucket (кастомный ключ):
```
Host bitbucket.org
  HostName bitbucket.org
  IdentityFile ~/.ssh/mykey
  ForwardAgent yes
```

Проброс ключа через форвардинг, выполнить в консоли до деплоя:
```
eval `ssh-agent -s`
ssh-add ~/.ssh/mykey
```
и проверка добавления:
```
ssh-add -L
```

Мультиключи на примере GitHub: https://gist.github.com/gubatron/d96594d982c5043be6d4


## Сбросить (спрятать) изменения для возможности коммита

Сбросить (спрятать) изменения локальной копии для коммита:
```
git stash
```

Удалить спрятанные изменения:
```
git stash drop
```

## Удалить коммит(ы)

Удалить последние коммиты в локальном репо:
```
git reset --hard <hash of needed commit>
```

А потом внести все изменения в origin (удаленный репо):
```
git push --force -u origin
```