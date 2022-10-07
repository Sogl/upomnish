# Deployer (PHP)

## .htaccess

Перенаправление на папку `current/public` (Laravel):
```
RewriteEngine on  
RewriteCond %{REQUEST_URI} !^/current/public  
RewriteRule ^(.*)$ /current/public/$1 [L]

RewriteCond %{HTTPS} off  
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# php -- BEGIN cPanel-generated handler, do not edit
# Set the “ea-php73” package as the default “PHP” programming language.
<IfModule mime_module>
  AddHandler application/x-httpd-ea-php73___lsphp .php .php7 .phtml
</IfModule>
# php -- END cPanel-generated handler, do not edit
```

Проще, перенаправление на `release`:
```
RedirectMatch ^/$ /release/
```