# git

## Клонировать инициализируя подмодули:
```
git clone --recurse-submodules git@repo.git
```

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

Вариант 2 — отмена для конкретного файла:
```
git checkout filename
```

## Удалить коммит(ы)

Удалить последние коммиты в локальном репо (!с осторожностью, может удалить локальные файлы):
```
git reset --hard <hash of needed commit>
```

А потом внести все изменения в origin (удаленный репо):
```
git push --force -u origin
```

## Удаление DS_Store

Команда покажет списком и удалит все DS_Store с проекта:
```
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

## Rebase, merge итп

Про слияние и перебазирование:
https://www.atlassian.com/ru/git/tutorials/merging-vs-rebasing

## Обновить gitignore

1. Make changes in `.gitignore` file.
2. Run `git rm -r --cached .` command.
3. Run `git add .` command
4. `git commit -m "Commit message"` or just `git commit` or continue working.

https://sigalambigha.home.blog/2020/03/11/how-to-refresh-gitignore/


## Получить изменения из продакшена, когда дев/локальная версия улетела вперед

1. Добавляем изменения: `git add .`
2. Коммитим: `git commit -m "My new commit"`
3. Получаем историю коммитов (!файлы при этом не изменяются): `git fetch origin`
4. Переносим наши изменения наверх истории: `git rebase origin/master`
5. Отправляем на git-хостинг: `git push origin master:master`
6. Остается только получить их в локальной версии: `git pull` или в приложении.