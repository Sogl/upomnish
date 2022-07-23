# .htaccess

## 301 редирект с домена на домен

```
RewriteEngine on
RewriteCond %{HTTP_HOST} ^(www\.)?mydomain\.tech$
RewriteRule ^(.*)$ http://mydomain.site/$1 [R=301,L]
```



Glavnaya stranica - default.html:
```
DirectoryIndex default.html
```

Svoya stranica oshibki 404
```
ErrorDocument 404 /404.html
```

Zakrit dostup dlya vseh
```
deny from all
```

Razreshit vhod tolko s adresa 208.77.188.166
```
Order deny,allow
Deny from all
Allow from 208.77.188.166
```

Perenapravlenie na sait test.com
```
Redirect / http://www.test.com
```

Zapret na otobrajenie failov v directorii pri otsutstvii indeksnogo faila
```
Options -Indexes
```

Otobrajenie failov v directorii pri otsutsvii indeksnogo faila
```
Options +Indexes
```

Ustanovit parol na directoriu
```
AuthName ProtectedZone
AuthType Basic
AuthUserFile /home/testuser/.htpasswd
require valid-user
```

Podderjka SSI v html
```
AddType text/html .shtml .htm .html
AddHandler server-parsed .shtml
Options +Includes
```


Privyazka domena subdomain.domain.ru k papke subdomain
```
RewriteEngine on
RewriteCond %{HTTP_HOST} (www\.)?subdomain\.domen\.ru$
RewriteCond %{REQUEST_URI} !^(/)?subdomain/
RewriteRule ^(.*)$ subdomain/$1
```

Obrabotka php v html
```
RemoveHandler .html .htm
AddType application/x-httpd-php .php .htm .html
```

Zapret dostupa s opredelennih IP
```
allow from all
Deny from 208.77.188.166
Deny from 82.98.86.174
```

Parol na ska4ivanie faila
```
<Files private.zip>
AuthName "Users zone"
AuthType Basic
AuthUserFile /home/testuser/.htpasswd
</Files>
```

Parol na gruppu failov(v primere dlya vse failov *.sql):
```
<Files "\.(sql)$">
AuthName "Protected zone"
AuthType Basic
AuthUserFile /home/testuser/.htpasswd
</Files>
```