# Timeweb

Для докера (Laradock):
```
###########################################################################
# ssh timeweb
###########################################################################


COPY timeweb /tmp/timeweb
COPY timeweb.pub /tmp/timeweb.pub

RUN rm -f /etc/service/sshd/down && \
    cat /tmp/timeweb.pub >> /root/.ssh/authorized_keys \
        && cat /tmp/timeweb.pub >> /root/.ssh/timeweb.pub \
        && cat /tmp/timeweb >> /root/.ssh/timeweb \
        && rm -f /tmp/timeweb* \
        && echo "Host aurum.timeweb.ru\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config \
        && chmod 644 /root/.ssh/authorized_keys /root/.ssh/timeweb.pub /root/.ssh/config \
    && chmod 400 /root/.ssh/timeweb \
    && cp -rf /root/.ssh /home/laradock \
    && chown -R laradock:laradock /home/laradock/.ssh
```





Запуск необходимой версии php в консоли:
```
/opt/php56/bin/php bin/grav clear-cache
```

Permissions:
https://getgrav.org/forum#!/getgrav/general:bingrav-permission-denied

Соединение по SSH с помощью ключей:
http://timeweb.com/ru/help//pages/viewpage.action?pageId=9241429

Со специальным именем файла подключаемся как:
```
ssh user@server.timeweb.ru -i timeweb
```

Конфигурация файла `config` для быстрого подключения:
```
Host timeweb
    HostName server.timeweb.ru
    User user
    IdentityFile ~/.ssh/timeweb
```

Как писать конфиги:
https://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/

Установка nodejs и npm:
https://timeweb.com/ru/help/pages/viewpage.action?pageId=8781927

Установка composer:
https://timeweb.com/ru/help/pages/viewpage.action?pageId=8781936


Пример моего `.bashrc` с npm, node, php 7.1, composer 1.7.0:
```
alias node='/home/u/user/nodejs/bin/node'

alias npm='/home/u/user/nodejs/bin/npm'

export PATH=$PATH:/home/u/user/nodejs/bin/

alias composer='/opt/php71/bin/php -d memory_limit=1024M /home/u/user/bin/composer'
alias php='/opt/php71/bin/php -d memory_limit=1024M'
```

Можно еще внести:
```
export PATH=/opt/plesk/php/7.1/bin:$PATH
```
